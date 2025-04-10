# Automatizar tareas diarias gracias a bash

## En investigacion

El siguiente directorio:
`~/.config/systemd/user/miscript.service`

Con el siguiente contenido:
```ini
[Unit]
Description=Mi Script al Iniciar Sesión

[Service]
ExecStart=/ruta/a/tu/script.sh
Restart=on-failure

[Install]
WantedBy=default.target
```

Habilitando el servicio:

```bash
systemctl --user daemon-reexec
systemctl --user enable --now miscript.service
```
