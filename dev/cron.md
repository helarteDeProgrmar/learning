# `cron` automatizar tareas

cron es una herramienta de Unix/Linux que permite programar la
ejecución automática de comandos o scripts en intervalos regulares
(minutos, horas, días, etc.). Se configura mediante el archivo `crontab`.

## Formato del fichero `crontab`

Para editarlo se ejecuta `crontab -e` y para ver las tareas que tiene
configuradas el usuario actual `crontab -l`

```txt
0 3 * * * /ruta/al/script.sh > archivo.log 2>&1
```

## Comando basicos

```bash
sudo systemctl enable crond
sudo systemctl start crond
systemctl status crond
```

## Alternativas a `cron`: `systemd`

Cron es una herramienta potente pero se ejecutan las cosas a nivel de usuario
Ahora es mas potente usar directamente `systemd`, de hecho cron es un servicio
dentro de este concept.

### Conceptos básicos de `systemd`

- *Unit (unidad)*: un archivo de configuracion que describe un servicio,
socket, montaje, tarea, etc.
- *Servicio*: algo que corre en segundo plano (por ejemplo nginx.service).
- *Timer*: reemplazo moderno de cron. Define cuándo ejecutar una tarea.
- *Target*: puntos de arranque (parecidos a los "runlevels" de SysV).

### Añadir una tarea (o servicio)

Para añadir una tarea crea un archivo en
`/etc/systemd/system/gnome-asdf.service`, y completa con un fichero de esta
forma:

```yml
[Unit]
Description=Ejecuta mi script personalizado

[Service]
Type=oneshot
ExecStart=/usr/local/bin/miscript.sh
```

A continuacion crear el timer, en `/etc/systemd/system/gnome-asdf.timer`

```yml
[Unit]
Description=Ejecutar mi script cada día a las 3:00 AM

[Timer]
OnCalendar=*-*-* 03:00:00
Persistent=true

[Install]
WantedBy=timers.target
```

Despues, tendras que reiniciar el demonio del sistema e ininiciar el servicio

### Comando utiles

```bash
sudo systemctl daemon-reload # Recargar systemd para reconocer nuevas unidades
sudo systemctl enable --now miscript.timer # Activar el timer
systemctl list-timers # Verificar que está activo
journalctl -u miscript.service -f # Ver los logs
sudo systemctl status miscript.service
```

### Explicacion de como funciona

Un servicio basicamente es un script que el sistema ejecuta en segundo plano.
Cuando le añdes un timer esta haciendo que el servicio comienze a determinadas
horas.

Si quieres tener un servicio y tu lanzarlo o pararlo manualmente, debes hacer:

```bash
sudo systemctl start gnome-asdf
sudo systemctl stop gnome-asdf
```

Cuando veas el status, veras si esta activo, inactivo o *failed* (la ultima vez
termino con error)

## Alternativas a `cron`: `at`

Al igual que `cron` depende del gran servicio de `systemctl`. Por ello para
comprobar que corre correctamente hay que ejecutar:

```bash
systemctl status atd
```

En resumen tenemos lo siguiente:

| Comando                | Función                             |
| ---------------------- | ----------------------------------- |
| `at [hora]`            | Programa una tarea                  |
| `atq`                  | Lista las tareas pendientes         |
| `atrm [id]`            | Elimina una tarea                   |
| `systemctl status atd` | Verifica si el servicio está activo |

hay que tener en cuenta el formato de la *"hora"*:

| **Formato**              | **Ejemplo**             | **Significado**                                         |
| ------------------------ | ----------------------- | ------------------------------------------------------- |
| `HH:MM`                  | `14:30`                 | A las 2:30 PM de hoy (si la hora ya pasó, será mañana). |
| `HH:MM YYYY-MM-DD`       | `14:30 2025-10-07`      | Fecha y hora exacta con año, mes y día.                 |
| `HH:MM [AM/PM]`                    | `10:00 PM`                                              | Hora en formato de 12 h. |
| `HH:MM tomorrow`         | `09:00 today`        | A las 9:00 de la mañana de mañana.                      |
| `HH:MM + número [minutes/hours/days/weeks]` | `now + 2 hours` | Dentro de un tiempo relativo (2 h desde ahora). |
| `now + tiempo`           | `now + 10 minutes`      | Ejecuta la tarea después del tiempo indicado.           |
| `midnight`               | `midnight`              | A las 00:00 del próximo día.                            |
| `noon`                   | `noon`                  | A las 12:00 del mediodía de hoy.                        |
| `teatime`                | `teatime`               | A las 16:00 (4 PM) — valor simbólico clásico de UNIX.   |
| `HH:MM MONTH DAY`        | `08:30 July 20`         | El 20 de julio a las 8:30.                              |
| `HH:MM MONTH DAY YEAR`   | `08:30 July 20 2026`    | Fecha y hora completa con año.                          |
| `MMDDYY`                 | `100625`                | 6 de octubre de 2025 a medianoche (00:00).              |
| `MM/DD/YY` o `DD.MM.YY`  | `10/06/25` o `06.10.25` | Variantes aceptadas del formato de fecha.               |
