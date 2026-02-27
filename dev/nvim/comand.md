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

---

## **Archivos y sesiones**

| Comando                | Descripción                                                        |
| ---------------------- | ------------------------------------------------------------------ |
| `:pwd`                 | Muestra el directorio actual                                       |
| `:cd <ruta>`           | Cambia el directorio actual                                        |
| `:lcd <ruta>`          | Cambia el directorio solo para la ventana local                    |
| `:browse e`            | Abre un diálogo de explorador de archivos                          |
| `:sav <archivo>`       | Guarda el archivo actual con otro nombre y lo sigue editando       |
| `:saveas <archivo>`    | Igual que `:sav`                                                   |
| `:mksession <archivo>` | Guarda la sesión actual (ventanas, buffers, etc.)                  |
| `:source <archivo>`    | Ejecuta un archivo Vimscript o init.lua                            |
| `:edit!`               | Recarga el archivo desde disco, descartando cambios                |
| `:checktime`           | Recarga archivos modificados externamente                          |
| `:args`                | Muestra los archivos en la lista de argumentos                     |
| `:argdo <cmd>`         | Ejecuta un comando en todos los archivos de la lista de argumentos |

---

## **Buffers y ventanas (profundizando)**

| Comando                | Descripción                                        |
| ---------------------- | -------------------------------------------------- |
| `:new`                 | Nueva ventana vacía (split horizontal)             |
| `:vnew`                | Nueva ventana vacía (split vertical)               |
| `:enew`                | Crea un nuevo buffer vacío                         |
| `:badd <archivo>`      | Añade un archivo a la lista de buffers sin abrirlo |
| `:bdelete`             | Cierra un buffer sin cerrar la ventana             |
| `:bwipeout`            | Elimina completamente un buffer                    |
| `:hide`                | Oculta la ventana actual (sin cerrar buffer)       |
| `:only`                | Cierra todas las ventanas excepto la actual        |
| `:resize <n>`          | Cambia la altura del split                         |
| `:vertical resize <n>` | Cambia el ancho del split                          |
| `:split` o `:vsplit`   | Divide la ventana actual                           |

---

## **Búsqueda avanzada**

| Comando                     | Descripción                                                                               |
| --------------------------- | ----------------------------------------------------------------------------------------- |
| `:vimgrep /patrón/ **/*.py` | Busca un patrón recursivamente en archivos (como grep)                                    |
| `:copen` / `:cclose`        | Abre / cierra la quickfix window (para mostrar resultados de búsqueda, compilación, etc.) |
| `:cnext` / `:cprev`         | Navega por los resultados de la quickfix                                                  |
| `:lvimgrep /patrón/ %`      | Igual que `:vimgrep` pero usa la **location list** (por ventana)                          |
| `:lopen` / `:lclose`        | Abre / cierra la location list                                                            |

---

## **Reemplazos y operaciones por rango**

| Comando                 | Descripción                                                         |
| ----------------------- | ------------------------------------------------------------------- |
| `:s/patrón/reemplazo/g` | Reemplaza en la línea actual                                        |
| `:.,$s/foo/bar/g`       | Reemplaza desde la línea actual hasta el final del archivo          |
| `:'<,'>s/foo/bar/g`     | Reemplaza en la selección visual                                    |
| `:%s/\<viejo\>/nuevo/g` | Reemplaza solo palabras completas                                   |
| `:g/patrón/cmd`         | Ejecuta `cmd` en todas las líneas que coinciden con `patrón`        |
| `:v/patrón/cmd`         | Ejecuta `cmd` en las líneas que **no** coinciden                    |
| `:global` / `:vglobal`  | Alias de `:g` / `:v`                                                |
| `:t` o `:copy`          | Copia líneas a otra posición (`:1,5t$` → copia líneas 1–5 al final) |
| `:m`                    | Mueve líneas (`:1,5m10` → mueve líneas 1–5 después de la línea 10)  |
| `:delete`               | Elimina líneas (`:1,3delete`)                                       |
| `:yank`                 | Copia líneas (`:1,3yank`)                                           |
| `:put`                  | Pega lo copiado                                                     |

---

## Configuración avanzada**

| Comando                  | Descripción                                          |
| ------------------------ | ---------------------------------------------------- |
| `:set`                   | Muestra todas las opciones modificadas               |
| `:set <opción>?`         | Muestra el valor actual de una opción                |
| `:setlocal <opción>`     | Cambia una opción solo para el buffer/ventana actual |
| `:setglobal <opción>`    | Cambia una opción globalmente                        |
| `:set no<opción>`        | Desactiva una opción booleana (`:set nowrap`)        |
| `:let var=value`         | Asigna variables en Vimscript                        |
| `:echo <expr>`           | Muestra el valor de una expresión o variable         |
| `:redir > archivo`       | Redirige la salida de comandos a un archivo          |
| `:scriptnames`           | Lista todos los scripts que Vim ha cargado           |
| `:verbose set <opción>?` | Muestra qué archivo o script cambió una opción       |

---

## **Macros, automatización y ejecución**

| Comando              | Descripción                                                                           |
| -------------------- | ------------------------------------------------------------------------------------- |
| `:@a`                | Ejecuta el contenido del registro `a` como comandos                                   |
| `:normal <cmd>`      | Ejecuta comandos de modo normal desde el modo comando                                 |
| `:normal! <cmd>`     | Igual que `:normal` pero ignora mapeos personalizados                                 |
| `:execute "comando"` | Evalúa y ejecuta texto como comando (`:execute "set " . var`)                         |
| `:source %`          | Ejecuta el archivo actual como script (muy útil para probar tu `.vimrc` o `init.lua`) |
| `:!<comando>`        | Ejecuta comandos del sistema                                                          |
| `:read !<comando>`   | Inserta la salida de un comando del sistema                                           |
| `:write !<comando>`  | Pasa el contenido del buffer a un comando (por ejemplo `:write !wc -l`)               |

---

## **Exploración e inspección**

| Comando        | Descripción                                  |
| -------------- | -------------------------------------------- |
| `:messages`    | Muestra los últimos mensajes de Vim          |
| `:reg`         | Muestra los registros (portapapeles)         |
| `:marks`       | Muestra las marcas                           |
| `:jumps`       | Muestra el historial de saltos               |
| `:changes`     | Muestra los cambios recientes                |
| `:undolist`    | Muestra el historial de deshacer             |
| `:scriptnames` | Muestra los scripts cargados                 |
| `:ls!`         | Lista todos los buffers, incluso los ocultos |
| `:display`     | Muestra el contenido de los registros        |

---

## **Neovim específico (Nvim 0.5+)**

| Comando                           | Descripción                                           |
| --------------------------------- | ----------------------------------------------------- |
| `:checkhealth`                    | Verifica la instalación y los plugins de Neovim       |
| `:lua <código>`                   | Ejecuta código Lua directamente                       |
| `:luafile <archivo>`              | Ejecuta un script Lua                                 |
| `:LspInfo`                        | Información del servidor LSP (si usas nvim-lspconfig) |
| `:Mason`                          | Abre el gestor Mason                                  |
| `:TSInstall <lenguaje>`           | Instala un parser de Tree-sitter                      |
| `:TSUpdate`                       | Actualiza todos los parsers                           |
| `:TSHighlightCapturesUnderCursor` | Muestra el grupo de highlight bajo el cursor          |
