# CLI de github

## Crear un repo

`gh repo create <repo-namrepo-namete] [OPTIONS]`

- [OPTIONS]:

1. `--private`

## Linkear un repo local con uno creado

`git remote add <remote-name> git@.../repo.git`


## Dar permisos a un usuario

```bash
gh api \
  -X PUT \
  -H "Accept: application/vnd.github+json" \
  /repos/OWNER/REPO/collaborators/USERNAME \
  -f permission=PERMISSION
```

### Reemplaza lo siguiente:

* `OWNER`: el nombre del propietario del repositorio (puede ser tú o una organización).
* `REPO`: el nombre del repositorio.
* `USERNAME`: el usuario al que quieres darle acceso.
* `PERMISSION`: uno de los siguientes niveles de acceso:

  * `pull` → solo lectura
  * `push` → lectura y escritura
  * `admin` → control total (incluye cambiar settings y gestionar colaboradores)
  * `maintain` → tareas de mantenimiento sin control total
  * `triage` → triage de issues y PRs, sin escritura

