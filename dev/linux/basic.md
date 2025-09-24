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
