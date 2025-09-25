# Basic commands in linux

En este fichero ire completando cosas que vaya aprendiendo basicas de linux y
algunos comandos curiosos.

## `dnf`

Empecemos como no por el gestor de paquetes:

```bash
sudo dnf check-update # actualizar lista de paquetes y ver cuales de los descargados tienen actualizaciones
sudo dnf update # actualizaciones de paquetes instalados
sudo dnf install paquete -y # no preguntar si continuar
sudo dnf install paquete1 paquete2 paquete3
sudo dnf install nombre_del_paquete --assumeno # simular descarga
sudo dnf install nombre_del_paquete --downlowadonly # simular descarga
sudo dnf remove nombre_del_paquete # eliminar/desinstalar paquetes
dnf search palabra_clave # busqueda de paquetes
dnf info nombre_del_paquete # informacion relevante del paquete
sudo dnf groupinstall "Development Tools" # Se pueden instalar grupos de paquetes
dnf history # bastante top
sudo dnf history undo <número_transacción>
sudo dnf clean all # limpiar cache
```

## globs

| Patrón              | Qué hace                                     | Ejemplo que coincide                                                  |
| ------------------- | -------------------------------------------- | --------------------------------------------------------------------- |
| `*`                 | Cualquier número de caracteres (excepto `/`) | `foo*` → `foo`, `foobar`, `foo123`                                    |
| `?`                 | Un solo carácter (excepto `/`)               | `?.txt` → `a.txt`, `b.txt`                                            |
| `[abc]`             | Uno de los caracteres listados               | `file[123].txt` → `file1.txt`, `file2.txt`                            |
| `[a-z]`             | Rango de caracteres                          | `file[a-c].txt` → `filea.txt`, `fileb.txt`                            |
| `[^abc]` o `[!abc]` | Cualquier carácter excepto los listados      | `file[!0-9].txt` → `filex.txt` pero no `file5.txt`                    |
| `**`                | Coincide recursivamente en subdirectorios    | `src/**/*.js` → encuentra todos los `.js` en `src/` y sus subcarpetas |

### Especificacion de `*` y `**`

Esto esta disponible en `zsh` y en `bash >= 4`

| Patrón       | Qué hace                                                  | Coincide con                     | No coincide con                  |
| ------------ | --------------------------------------------------------- | -------------------------------- | -------------------------------- |
| `*`          | Cualquier cosa en el mismo nivel                          | `file1.txt`, `notes.md`          | `src/main.c`, `src/utils/test.c` |
| `src/*`      | Archivos directos dentro de `src/`                        | `src/main.c`, `src/helper.c`     | `src/utils/test.c`               |
| `src/**/*.c` | Todos los `.c` dentro de `src/`, sin importar profundidad | `src/main.c`, `src/utils/test.c` | `file1.txt`, `notes.md`          |
| `**/*.txt`   | Todos los `.txt` en cualquier subdir                      | `file1.txt`                      | `src/main.c`                     |

