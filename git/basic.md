# Introducción

En este documento se enumeran y explican brevemente los principales y
más usados comandos de git con sus correspondientes opciones,
incluyendo ejemplos prácticos de uso.

## Control historia: `git status` y `git log`

### `git log`

- `-n 10`
- `-grahp`
- `--nopager`
- `--oneline`
- `-p`: ver las diferencias
- `--pretty`: ver autor del commit

## Configuración: `git config`

### `--local`

Establece la configuración únicamente para el repositorio actual.

- **Ejemplo**: `git config --local user.name "Manolo Caracol"`

### `--global`

Establece la configuración para el usuario en todos los repositorios.

- **Ejemplo**: `git config --global user.email "manolocaracol@example.com"`

### Ver la configuracion local

```txt
git config --local --list
git config --list
git config --global --list
```

O tambien verlo en los ficheros de configuracion: `.git/config`, `~/.gitconfig`

### Opciones interesantes

- **`user.name`**: Define el nombre del usuario.
- **`user.email`**: Define el correo electrónico.
- **`core.editor`**: Establece el editor de texto por defecto.
- **`color.ui`**: Activa la coloración en la salida de comandos.

## `git add`

- **básico**: `git add archivo.txt`
- **interactivo**: `git add archivo.txt -p`
- **para todos los archivos modificados**: `git add .`
- **para los archivos traqueados**: `git add -u`

## `git commit`

Guarda los cambios del área de preparación en el repositorio.

- **con mensaje**: `git commit -m "Agrega nueva funcionalidad"`
- **para modificar el último commit**: `git commit --amend -m "Mensaje corregido"`

## `git branch`

- **ver ramas**: `git branch`
- **ver ramas locales y remotas**: `git branch -a`
- **cambiar traqueado rama**:
```git branch <local-branch-name> --set-upstream-to <remote-name>/<remote-branch-name>```
- **segun warning de git**: `git branch --set-upstream-to=<remote>/<branch> master`
- **crear rama remoto**: ```git push <remote-name> <local-branch-name>:<remote-branch-name>```
- **borrar rama en remoto**: ```git push origin --delete nombre-rama```
- **ver ramas y su upsteam**: ```git branch -vv```
- **rama protegida por remoto**: 
    * bitbucket: Ve a `repo>repositoty settings>repository details>advanted` y
    selecciona la rama principal. Despues ve a `branching model`

## `git switch` vs `git checkout`

`git switch` es el comando moderno y específico para cambiar de rama,
simplificando el uso.

- **con switch**: `git switch develop`
- **con switch**: `git switch -c nueva-rama`
- **con switch**: `git switch -d rama-a-borrar`
- **con switch**: `git switch -D rama-a-borrar` (borra sin preguntar)

`git checkout` es más versátil, ya que permite cambiar de rama o restaurar archivos.

- **para cambiar a una rama existente**: `git checkout develop`
- **para crear y cambiar a una nueva rama**: `git checkout -b nueva-rama`

## `git merge`

Une el historial de dos ramas, integrando cambios de una rama en la actual.

- **básico**: `git merge feature`
- **con opción --no-ff**: `git merge --no-ff feature`

Cuando hay conflictos:

- **quedarse con cambios locales**: `git checkout --ours .`
- **quedarse con cambios del rama que viene**: `git checkout --theirs .`
Después completar con `git add. && git commit`

Antes de probocar conflictos:

- Mirar diferencias: `git diff rama1..rama2`
- Ver que problemas van a existir: `git merge --no-commit --no-ff main`

## `git rebase`

Te situas en la rama que quieres actualizar, por ejemplo desde feature1
a develop. Escribes el comando `git rebase develop` y se actualiza el commit origen
de esta rama.

- **básico**: `git rebase master`
- **interactivo para reordenar o combinar commits**: `git rebase -i HEAD~3`

### Conflictos rebase

- **parar, deshacer, abortar**: `git rebase --abort` tambien
en problemas con `git pull --rebace`
- **quedarse con locales**:

## `git revert`

Crea un nuevo commit que deshace los cambios de un commit anterior,
sin modificar la historia existente.

- **Ejemplo**: `git revert abc1234`  
  (donde `abc1234` es el hash del commit a revertir)

## `git reset`

Restablece el puntero HEAD a un commit anterior,
pudiendo modificar el área de staging y/o el working directory.

- **con --soft**: `git reset --soft HEAD~1`
- **con --hard**: `git reset --hard HEAD~1`

## `git restore`

Permite restaurar archivos a su estado previo,
ya sea desde el repositorio o del área de staging.

- **para restaurar un archivo del working
directory**: `git restore archivo.txt`
- **para eliminar un archivo del área de
staging**: `git restore --staged archivo.txt`

## `git revert` vs `git reset`

- **`git revert`**: Añade un commit que deshace cambios,
preservando la historia del repositorio.
  - **Ejemplo**: `git revert abc1234`
- **`git reset`**: Mueve el puntero HEAD a un commit anterior,
lo que puede reescribir la historia y eliminar commits posteriores.
  - **Ejemplo**: `git reset --hard HEAD~1`

Es interesante utilizar revert cuando quiero conservar los cambios
de una rama muy grande. Si se encuentra un bug en algo en producción quizas
no se quiere perder lo que se había avanzado pero se quiero volver a un momento
anterior. Todo depende de como se gestione la historia en el equipo.

## `git remote`

Gestiona las conexiones con repositorios remotos, facilitando la colaboración.

- **para añadir un repositorio remoto**: `git remote add origin url`
- **para listar remotos**: `git remote -v`

Es interesante ver la estructura del mandato:
```git remote add nombre-remoto url```
Pudiendo ser el remoto por ejemplo una dirección del local.
Pensar que el remoto simplemente es un repositorio mas de git.

### `git push/pull`

- **`git push`**: Envía los commits locales al repositorio remoto.
  - **Ejemplo**: `git push origin master`
- **`git pull`**: Trae y fusiona cambios desde el repositorio remoto al local.
  - **Ejemplo**: `git pull origin master`
- **subir bajar lo commiteado y añadir mis commits acontinuación**: `git pull --rebase`

## `git cherry-pick`

Permite aplicar uno o varios commits específicos de
otra rama a la rama actual, sin necesidad de hacer un merge completo.

- **Ejemplo**: `git cherry-pick abc1234`  
  (para aplicar el commit identificado por `abc1234`)
- **que en el commit aparezca que es cheery**: añadir el sigueinte
flag `git cherry-pick abc1234 -x`

## `git stash`

Guarda temporalmente cambios no confirmados
para poder trabajar en otra cosa sin perderlos.

- **para guardar cambios**: `git stash save "trabajo en progreso"`
- **para aplicar y eliminar el último stash**: `git stash pop`

## `git squash`

Combina múltiples commits en uno solo para limpiar el historial del repositorio.

- **Ejemplo**: Utilizar `git rebase -i` y cambiar "pick"
a "squash" en los commits que se quieran combinar.

## `git tag`

- **para crear un tag en el commit actual**: `git tag <tag-name>`
- **para crear un tag anotado**: `git tag -a v1.0 -m "Versión 1.0"`
- **idem otra manera**: `git tag v1.0 -m "Versión 1.0"`
- **para subir tags**: `git push --tags`
- **para listar tags**: `git tag`
- **para eliminar tags**: `git tag -d <tag>`
- **para eliminar tags del remoto**: `git push <nombre-remote> --delete <tag>`

## `git bisect`

- **para iniciar el proceso**: `git bisect start`
- **para marcar un commit como bueno**: `git bisect good abc1234`
- **para marcar un commit como malo**: `git bisect bad def5678`

## Worktrees

- **para añadir un worktree**: `git worktree add ../ruta-nueva-rama develop`

## Clone

- **Clona repo de toda la vida** `git clone <repo-url>`
- **Clona repo con nombre cambiado** `git clone <repo-url> <new-name>`

## Blame, ver historial

- **ver historial de un fichero**: `git blame file-name`
- **ver commit de una o varias lineas**: `git blame file-name -L 1,10`
- **ver commit y metadatos de una linea**: `git blame file-name -L 1,1 --incremental`
- **ver historial de un fichero**: `git log --follow -p [filename]`
