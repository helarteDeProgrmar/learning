# Comando utiles desde modo `comand`

## Navegación y manejo de archivos

| Comando        | Acción                                           |
| -------------- | ------------------------------------------------ |
| `:e <archivo>` | Abre un archivo (por ejemplo: `:e index.html`)   |
| `:w`           | Guarda el archivo actual                         |
| `:w <archivo>` | Guarda como (por ejemplo: `:w nuevo.txt`)        |
| `:q`           | Sale de Vim (solo si no hay cambios sin guardar) |
| `:q!`          | Sale **sin guardar**                             |
| `:wq`          | Guarda y sale                                    |
| `:x`           | Guarda y sale (igual que `:wq`)                  |
| `:qa`          | Cierra todos los archivos abiertos               |
| `:wa`          | Guarda todos los archivos abiertos               |
| `:wqa`         | Guarda y cierra todo                             |

---

## Búsqueda y reemplazo

| Comando              | Acción                                                        |
| -------------------- | ------------------------------------------------------------- |
| `:/texto`            | Busca “texto” hacia adelante                                  |
| `:?texto`            | Busca “texto” hacia atrás                                     |
| `:s/viejo/nuevo/`    | Reemplaza **solo la primera coincidencia** en la línea actual |
| `:s/viejo/nuevo/g`   | Reemplaza **todas** las coincidencias en la línea actual      |
| `:%s/viejo/nuevo/g`  | Reemplaza en **todo el archivo**                              |
| `:%s/viejo/nuevo/gc` | Reemplaza en todo el archivo **confirmando cada cambio**      |

---

## Navegación entre buffers, ventanas y pestañas

| Comando             | Acción                                   |
| ------------------- | ---------------------------------------- |
| `:ls` o `:buffers`  | Lista los buffers abiertos               |
| `:b <n>`            | Cambia al buffer número *n*              |
| `:bn` / `:bp`       | Siguiente / anterior buffer              |
| `:sp <archivo>`     | Abre un archivo en **split horizontal**  |
| `:vsp <archivo>`    | Abre un archivo en **split vertical**    |
| `:close`            | Cierra la ventana actual                 |
| `:tabnew <archivo>` | Abre un archivo en una **nueva pestaña** |
| `:tabn` / `:tabp`   | Navega entre pestañas                    |

---

## Configuración y ayuda

| Comando               | Acción                                          |
| --------------------- | ----------------------------------------------- |
| `:set number`         | Muestra los números de línea                    |
| `:set relativenumber` | Números relativos (muy usado en Neovim)         |
| `:set ignorecase`     | Ignora mayúsculas/minúsculas al buscar          |
| `:set smartcase`      | Sensible a mayúsculas solo si escribes alguna   |
| `:syntax on`          | Activa el resaltado de sintaxis                 |
| `:syntax off`         | Desactiva el resaltado de sintaxis              |
| `:help`               | Abre la ayuda de Vim                            |
| `:help <tema>`        | Ayuda sobre un tema específico (ej: `:help :w`) |

---

## Misceláneo útil

| Comando         | Acción                                                       |
| --------------- | ------------------------------------------------------------ |
| `:!<comando>`   | Ejecuta un comando del sistema (ej: `:!ls`)                  |
| `:r <archivo>`  | Inserta el contenido de otro archivo en el actual            |
| `:r !<comando>` | Inserta la salida de un comando del sistema (ej: `:r !date`) |
| `:noh`          | Elimina el resaltado de búsquedas                            |
