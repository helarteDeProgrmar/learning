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
