# Fork

Copia del repositorio original en tu cuenta GitHub para poder trabajar sin
permisos.

---

## Flujo de trabajo típico

| Acción                  | Resultado                 |
| ----------------------- | ------------------------- |
| Crear fork en github    | Nuevo repo en tu cuenta   |
| Fork del repositorio    | Tienes tu copia           |
| Clonar tu fork          | Repo en tu PC             |
| Crear branch            | Espacio seguro de trabajo |
| Hacer cambios + commits | Historial claro           |
| Push a tu fork          | Cambios en GitHub         |
| Crear Pull Request      | Propones cambios          |
| Sincronizar fork        | Te mantienes actualizado  |

---

## Comandos esenciales

### basicos

| Acción             | Comando                                               |
| ------------------ | ----------------------------------------------------- |
| Clonar tu fork     | `git clone https://github.com/tu-usuario/tu-fork.git` |
| Entrar al proyecto | `cd tu-fork`                                          |
| Crear rama         | `git checkout -b mi-feature`                          |
| Ver ramas          | `git branch`                                          |
| Subir cambios      | `git push origin mi-feature`                          |

### Mantener el repo actualizado

| Objetivo                           | Comando                                                            |
| ---------------------------------- | ------------------------------------------------------------------ |
| Añadir repo original como upstream | `git remote add upstream https://github.com/original/proyecto.git` |
| Ver remotos configurados           | `git remote -v`                                                    |
| Traer cambios del original         | `git fetch upstream`                                               |
| Cambiar a main                     | `git checkout main`                                                |
| Actualizar main (merge)            | `git merge upstream/main`                                          |
| (o) Actualizar main (rebase)       | `git rebase upstream/main`                                         |
| Subir main actualizado a tu fork   | `git push origin main`                                             |
