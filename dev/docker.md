# Docker

## Manejo de las imagenes y dockerhub

```bash
docker search nombre_o_palabra_clave # buscar imagenes en dockerhub
docker pull nombre_imagen # descargar imagenes
docker inspect nombre_imagen # ver detalles de la imagen ya descargada
docker run --rm -it nombre_imagen
docker images # ver imagen descargadas
docker rmi nombre_de_la_imagen # borrar imagen
docker image rm nombre_de_la_imagen # borrar imagen
docker rmi -f nombre_de_la_imagen # borrarla aunquee este en uso
```

## docker compose vs docker

Es importante entender la diferencia. Ambos son herramientas que tiene cli.
La clave esta en entender que docker es la plataforma de contenedores que
permite empaquetar una aplicacion. El comando docker por si solo, solo permite
interactuar con un solo contenedor.

Mientras `docker compose` permite definir y manipular aplicaciones
multicontenedor.

### Uso de docker compose

- `docker-compose up`
Levanta y crea todos los servicios definidos en el archivo docker-compose.yml.
Puedes usar el flag -d para ejecutarlo en segundo plano.
- `docker-compose down`
Detiene y elimina los contenedores, redes y volúmenes creados por
docker-compose up.
- `docker-compose ps`
Lista los contenedores y servicios gestionados por Compose.
- `docker-compose logs servicio`
Muestra los logs de uno o varios servicios.
- `docker-compose build`
Construye o reconstruye las imágenes de los servicios definidos en el archivo.
