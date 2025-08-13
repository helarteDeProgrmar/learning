# Procesos Linux

En este nuevo fichero vamos a refrescar algunos conceptos básicos sobre
procesos y comandos importantes, útiles y curiosos.

Antes de nada, recordar que siempre toda la información sobre
los ficheros de procesos se guarda en el directorio `/proc/`.
Este directorio virtual es crucial; cada subdirectorio con un nombre
numérico corresponde al **PID (ID de proceso)** de un proceso
en ejecución. Por ejemplo, el directorio `/proc/1234`
contendría información sobre el proceso con PID 1234.

---

## Comandos

Evidentemente hay que recordar:

- `top`, y algunas de sus variantes o nuevas herramientas como `htop`. Estas herramientas son monitores de procesos interactivos que te permiten ver en tiempo real el uso de CPU, memoria y otros recursos por cada proceso. 

- `ps` con algunos flags como `aux`, `-u <user>`. El comando `ps` (process status) muestra una instantánea de los procesos que se están ejecutando.
  - `ps aux`: Muestra todos los procesos de todos los usuarios en el sistema, incluyendo los que no tienen una terminal asociada. Las columnas que muestra son `USER`, `PID`, `%CPU`, `%MEM`, `VSZ`, `RSS`, `TTY`, `STAT`, `START`, `TIME`, y `COMMAND`. Es una de las combinaciones más usadas.
  - `ps -u <user>`: Muestra todos los procesos que pertenecen a un usuario específico.

- `pstree`, un comando muy guapo para investigar y aprender. `pstree` muestra los procesos en una vista de árbol jerárquica, lo que te ayuda a entender las relaciones de padre e hijo entre los procesos. Un proceso padre puede iniciar uno o varios procesos hijos. 

### Más comandos importantes y curiosos

Además de los que ya mencionaste, estos comandos son fundamentales para la gestión de procesos:

- `kill <PID>`: Envía una señal (por defecto `SIGTERM`,
pide "amablemente" terminar). `kill -9 <PID>`, envía la señal `SIGKILL`

- `killall <nombre_proceso>`: Mata todos los procesos con mismo nombre, ej. `killall firefox`

- **`jobs`**: ver los procesos iniciados en esa terminal que están en
segundo plano o suspendidos. `fg <número_job>` traer un proceso al primer plano,
o `bg <número_job>` para ponerlo en segundo plano si está suspendido.

- **`nohup`**: ejecutar un comando que ignore señales de
colgado (`SIGHUP`). Esto es muy útil cuando ejecutas un
script o programa en segundo plano y quieres que siga funcionando
incluso si cierras la terminal. Ejemplo: `nohup tu_script.sh &`.

- **`pgrep`**: encontrar PIDs basándose en un patrón. Por ejemplo, `pgrep firefox`


## Buscar y matar proceso

1.  Usa `ps aux | grep <nombre_del_programa>` o `pgrep <nombre_del_programa>` para encontrar su PID.
2.  Si el PID es, por ejemplo, `1234`, intenta terminarlo amablemente: `kill 1234`.
3.  Si no se cierra, fuerza el cierre: `kill -9 1234`.

## Procesos huérfanos y procesos zombis

Para entender cómo un proceso puede perdurar, es importante conocer dos estados curiosos que pueden adquirir los procesos:

### Proceso huérfano

Un **proceso huérfano** es aquel cuyo **proceso padre ha terminado antes que él**. Cuando esto sucede, el sistema operativo no deja al proceso hijo sin supervisión. El proceso **`init`** (o `systemd` en sistemas modernos), que es el primer proceso que se ejecuta al arrancar el sistema con PID 1, se convierte en el nuevo padre del proceso huérfano. `init` se encarga de "adoptar" a los huérfanos y de gestionar su finalización cuando terminan su trabajo, evitando que se queden en el limbo.

**¿Cuándo puede ocurrir?**

  - Cuando cierras la terminal mientras un proceso hijo (por ejemplo, un editor de texto o un script) sigue en ejecución en segundo plano sin usar **`nohup`**. Si el proceso hijo no recibe la señal **SIGHUP** correctamente o la ignora, el proceso padre (la shell) muere y el hijo es adoptado.

### Proceso zombi

Un **proceso zombi** (también conocido como **defunct**) es un proceso que ya ha terminado su ejecución, pero su entrada en la tabla de procesos aún no ha sido eliminada. Esto ocurre porque el proceso padre aún no ha leído su estado de salida. El proceso zombi no consume recursos de CPU ni memoria, pero sigue ocupando un PID. Si se acumulan muchos procesos zombis, se pueden agotar los PIDs disponibles, lo que puede ser un problema.

**¿Cuándo puede ocurrir?**

  - Esto suele suceder cuando un proceso padre falla al llamar a la función **`wait()`** para leer el estado de salida de su hijo. El proceso padre es el responsable de "cosechar" a los procesos zombis para que el sistema operativo pueda liberar el PID.
  - Si el proceso padre muere antes de "cosechar" a su hijo, el hijo zombi es adoptado por **`init`**, que se encarga de liberar el PID correctamente.

En resumen, los **huérfanos** son procesos vivos cuyo padre ha muerto, mientras que los **zombis** son procesos muertos cuyo padre aún no ha leído su estado de salida.

