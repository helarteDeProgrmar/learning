# Grouop

Es interesante que existen grupos para un ordenador con un
solo usuario aparentemete.

Pero evidentemte hay mas, root, docker...

## Ver a que grupo se pertenece

Con tu usuario actual puedes ver a que grupos perteneces: `groups`

Para ver todos los grupos dentro de un ordenador: `getent group`
Para cargar la shell de nuevo con <group> como grupo primario: `newgrp docker`

Ver los usuarios a lo bruto: `cut -d: -f1 /etc/passwd`
Ver solo usuario especifico: `getenv passwd rgpb`
