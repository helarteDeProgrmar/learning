# Users and Groups

Es interesante que existen grupos para un ordenador con un
solo usuario aparentemete.

Pero evidentemte hay mas, root, docker...

## Gestion de permisos

1. Gestión de usuarios y grupos avanzados

*Conceptos clave:*

- Usuarios: identificados por un UID (User ID).
- Grupos: cada usuario puede pertenecer a uno o más grupos (GID).

Archivos importantes:

```txt
/etc/passwd → información básica del usuario.
/etc/shadow → contraseñas cifradas.
/etc/group → definición de grupos.
```

## Users

### Eliminacion de usuarios

1. Revisamos si usuario tiene procesos activos:

```bash
ps -u nombre_usuario
sudo pkill -u nombre_usuario # matamos en caso de quee existan
```

2. Borrar:

```bash
sudo userdel -r nombre_usuario
```

Si el usuario habia creado archivos a lo largo del dispositivo los puedes
eliminar con:

```bash
sudo find / -user nombre_usuario -exec rm -rf {} \;
```

3. Comprobacion, verifica que la salida de esto da un error:

```bash
id nombre_usuario
```

## Grupos

### Ver a que grupo se pertenece

Con tu usuario actual puedes ver a que grupos perteneces: `groups`

Para ver todos los grupos dentro de un ordenador: `getent group`
Para cargar la shell de nuevo con <group> como grupo primario: `newgrp docker`

Ver los usuarios a lo bruto: `cut -d: -f1 /etc/passwd`
Ver solo usuario especifico: `getenv passwd rgpb`
