# Documentación de `curl` y sus Opciones

Este documento contiene una recopilación de las opciones más útiles de
`curl` para interactuar con recursos web, realizar solicitudes HTTP,
manejar autenticación y más.

## Introducción

`curl` es una herramienta de línea de comandos utilizada para hacer
solicitudes a servidores web. Es útil para automatizar la descarga de recursos,
interactuar con APIs, y manejar autenticación, cookies y otros parámetros de solicitud.

## Opciones Básicas


```bash
curl https://example.com # muestra el contido por terminal
curl -O https://example.com/file.txt # decarga fichero y lo llama igual que el remoto
curl -o archivo.txt https://example.com/file.txt
curl -O https://example.com/file1.txt -O https://example.com/file2.txt # descarga varios
curl -i https://example.com # mustra encabezados y contenido
curl -I https://example.com # muentra solo encabezados
curl -u username:password https://example.com # autenticacion basica contraseña usuario
curl -c cookies.txt -X GET https://example.com # autenticacion guarda las 
# cookies en un archivo
curl -b cookies.txt -X GET https://example.com # coge las cookies de un archivo
curl -H "Authorization: Bearer <tu_token>" https://example.com/protected-resource
curl -X POST -d "param1=value1&param2=value2" https://example.com/formulario
curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' https://example.com/api
curl -X POST -F "file=@archivo.txt" https://example.com/upload
curl --max-time 30 https://example.com # timeout solicitud entera
curl --connect-timeout 10 https://example.com # timeout conexion
```

## Opciones avanzadas

```bash
cat urls.txt | xargs -n 1 -P 4 curl -O # descarga paralelamente varios ficheros
```
