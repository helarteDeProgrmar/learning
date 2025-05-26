# Problemas típicos en git

## Conflictos al mergear:

Para solucionar este problema se puede visitar el enlace:
```txt
https://support.atlassian.com/bitbucket-cloud/docs/resolve-merge-conflicts/
```

## Borrar un fichero de la historia

Ver el enlace y documentar mejor este punto proximamente:

[enlace a pagina con info](https://dev.to/matiasfha/git-como-eliminar-un-archivo-de-la-historia-mpp)

## Ver diferencias entre ramas

```bash
git diff <rama1> <rama1> -- <file_nanme>
```

## Squasear commits de la historia

1. **Identifica el rango de commits**  

   Supongamos que tienes esta secuencia y quieres agrupar 
   los tres commits marcados en uno solo:  

   ```txt
   A — B — C — D — E — F — G  (rama “master”)
               ↑   ↑   ↑
             commit1 commit2 commit3
   ```  

   Debes indicar al rebase interactivo que comience justo **antes**
   de `commit1`. Si `commit1` es, por ejemplo, `D`, harías:

   ```bash
   git checkout master
   git rebase -i D^
   ```

2. **Edita la lista en tu editor**  
   Se abrirá un fichero con algo así:

   ```txt
   pick ddddddd commit1
   pick eeeeeee commit2
   pick fffffff commit3
   pick ggggggg commit4
   pick hhhhhhh commit5
   ```

   Cambia la palabra `pick` por `squash` (o su abreviatura `s`) en **todos salvo el primero** de los commits que quieras unir. Por ejemplo:

   ```txt
   pick ddddddd commit1
   squash eeeeeee commit2
   squash fffffff commit3
   pick ggggggg commit4
   pick hhhhhhh commit5
   ```

   > Lo que hace es “tomar” el commit1 como base y “aplastar” (`squash`)
   encima los commit2 y commit3.

3. **Guarda y cierra el editor**  
   Git te ofrecerá un segundo editor para combinar los mensajes de commit.
  Ajusta al mensaje definitivo que desees y guarda.

4. **Resuelve conflictos si aparecen**  
   Si al juntar esos cambios hay conflictos, Git te lo indicará. Resuélvelos manualmente, luego:

   ```bash
   git add <archivos-resueltos>
   git rebase --continue
   ```

5. **Actualiza el repositorio remoto (si aplica)**  
   Como has reescrito la historia, deberás forzar el push:

   ```bash
   git push --force-with-lease origin master
   ```

   Usa `--force-with-lease` para asegurarte de no pisar cambios ajenos por error.


## Cambiar metadatos commits

Estudiar cosas interesantes y dudas:

- Los hash los crea a partir de los datos del commit y los anteriores commits.
Hay algun problema si cambio los metadatos?

```bash
# Crea un commit de prueba:
git commit --allow-empty -m "Hola, mundo"

# Obtén su hash (por ejemplo abc1234...):
hash=$(git rev-parse HEAD)

# Muestra el contenido sin comprimir:
git cat-file -p $hash
```

Salida:

```txt
tree d670460b4b4aece5915caf5c68d12f560a9fe3e4
author Alice <alice@example.com> 1716422400 +0200
committer Alice <alice@example.com> 1716422400 +0200

Hola, mundo
```

### git cat-file

Es un comando interesante, tiene las siguientes opciones:

```bash
git cat-file -p <hash> # tenemos que sacar el hash sacando los metadatos del commit
git cat-file commit <commit-hash> # tenemos que pasar la referencia del commit
```

El comando contrario es `git `




## REVISAR




Aquí tienes un ejemplo de cómo podrías implementar el paso 4 de manera semiautomática, iterando sobre cada commit, permitiéndote editar los metadatos (autor, committer, mensaje…) y creando en su lugar nuevos objetos:

```bash
#!/usr/bin/env bash
set -e

# 0) Haz una copia de seguridad de tu rama por si algo sale mal
git branch backup-main

# 1) Prepara un fichero donde guardaremos el mapeo old→new
mapfile="commit-map.txt"
> $mapfile

# 2) Variables de control
new_parent=""

# 3) Itera de más antiguo a más reciente
for old in $(git rev-list --reverse HEAD); do
  echo "Procesando commit $old …"

  # 3.a) Extrae el contenido crudo del commit
  git cat-file commit $old > tmp-commit.txt

  # 3.b) Ajusta la referencia al padre:
  if [ -n "$new_parent" ]; then
    # si hay padre nuevo, reemplaza la línea parent
    sed -i "s/^parent .*/parent $new_parent/" tmp-commit.txt
  else
    # commit inicial: elimina cualquier línea parent
    sed -i "/^parent /d" tmp-commit.txt
  fi

  # 3.c) Abre el objeto en tu editor para modificar AUTHOR, COMMITTER o mensaje
  ${EDITOR:-vi} tmp-commit.txt

  # 3.d) Crea el nuevo objeto commit y captura su hash
  new=$(git hash-object -t commit -w tmp-commit.txt)
  echo " → Nuevo commit: $new"

  # 3.e) Guarda el mapeo y actualiza new_parent para el siguiente ciclo
  echo "$old $new" >> $mapfile
  new_parent=$new
done

# 4) Mueve la rama (por ejemplo, main) al último commit reescrito
git update-ref refs/heads/main $new_parent

echo "Historia reescrita. Mapeos old→new en $mapfile"
echo "Revisa con 'git log' y, si todo está OK, limpia objetos huérfanos:"
echo "  git reflog expire --expire=now --all"
echo "  git gc --prune=now --aggressive"
```

---

### Explicación de cada bloque

1. **Backup**
   Antes de tocar nada en tu historial real, creas `backup-main` apuntando a donde estás ahora.

2. **Listado de commits**
   `git rev-list --reverse HEAD` te da todos los commits desde el inicial hasta el actual, en orden cronológico.

3. **Procesamiento por commit**

   * **`git cat-file commit $old`** volca el objeto crudo a `tmp-commit.txt`.
   * **Ajuste de padre**: para que la cadena de commits siga siendo coherente, cada nuevo commit debe apuntar como padre al hash que hemos generado en la iteración anterior (`new_parent`).
   * **Edición manual**: abres `tmp-commit.txt` en `$EDITOR` para que cambies campos `author …`, `committer …` y/o el mensaje.
   * **`git hash-object -t commit -w`** comprime y almacena tu nuevo texto como un objeto Git, devolviendo el nuevo hash.
   * Guardas en `commit-map.txt` el par “viejo nuevo” por si tienes que consultarlo luego.

4. **Reasignar la rama**
   Al final, mueves `main` (o la rama que quieras) al hash del último commit reescrito. A partir de ahí, tu historia mostrará sólo los nuevos commits con los metadatos que hayas introducido.

5. **Limpieza** *(opcional)*
   Los viejos commits quedan huérfanos y, tras expirar reflogs y hacer `git gc`, se eliminarán del repositorio.

---

**Advertencias finales**

* Esta operación **reescribe** la historia. Evita hacerlo en ramas compartidas sin avisar y prepárate a forzar el push (`git push --force`).
* Siempre ten un respaldo (como la rama `backup-main`) hasta que confirmes que todo funciona.
* Si necesitas repetir o variar algo, revisa `commit-map.txt` para asociar hashes antiguos y nuevos.

