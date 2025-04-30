# Problemas típicos en git

## Conflictos al mergear:

Para solucionar este problema se puede visitar el enlace:
```txt
https://support.atlassian.com/bitbucket-cloud/docs/resolve-merge-conflicts/
```

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
