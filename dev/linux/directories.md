| Carpeta          | Contenido principal                                                             |
| ---------------- | ------------------------------------------------------------------------------- |
| `/`              | Punto de entrada del sistema; sólo subdirectorios esenciales.                   |
| `/bin`           | Ejecutables esenciales para todos los usuarios (p. ej. `ls`, `cp`, `bash`).     |
| `/sbin`          | Ejecutables del sistema/administración (p. ej. `fdisk`, `iptables`).            |
| `/lib`, `/lib64` | Bibliotecas compartidas usadas por `/bin` y `/sbin`.                            |
| `/etc`           | Archivos de configuración global del sistema y de servicios.                    |
| `/dev`           | Archivos de dispositivos (discos, puertos, terminales).                         |
| `/proc`          | Sistema de archivos virtual con información del kernel y procesos en ejecución. |
| `/sys`           | Sistema de archivos virtual para interactuar con el kernel (sysfs).             |
| `/run`           | Datos volátiles en tiempo de ejecución (PID files, sockets).                    |
| `/tmp`           | Archivos temporales de corta vida; se pueden eliminar al reiniciar.             |
| `/var`           | Datos variables:                                                                |

* `/var/log`: registros de logs
* `/var/lib`: bases de datos y datos de aplicación
* `/var/cache`: cachés persistentes
* `/var/spool`: colas de impresión, correo, etc.          |
  \| `/home`              | Directorios personales de usuarios (`/home/usuario`).                               |
  \| `/srv`               | Datos de servicios ofrecidos (sitio web, FTP, etc.).                                |
  \| `/boot`              | Archivos de arranque (kernel, initrd, config de GRUB).                              |
  \| `/mnt`               | Puntos de montaje **manual** y temporales para particiones o dispositivos.          |
  \| `/media`             | Puntos de montaje **automático** para medios extraíbles (CD, USB).                  |
  \| `/opt`               | Software opcional o de terceros, empaquetado aparte del sistema base.               |
  \| `/usr`               | Software de usuario de sólo lectura y documentación:
* `/usr/bin`, `/usr/sbin` (ejecutables)
* `/usr/lib` (librerías)
* `/usr/share` (archivos compartidos)          |
  \| `/usr/local`         | Software instalado manualmente (compilado o binarios de terceros) sin interferir con el gestor de paquetes. |
