# Connect to mongo server running in a server 

## Añadir un elemento con indice, sustituir si existe

```python
db.tuColeccion.replaceOne(
  { clave: valorUnico },           # filtro para encontrar el documento existente
  { clave: valorUnico, ...otrosDatos },  # documento nuevo que se insertará o reemplazará
  { upsert: true }
)
```


```
ssh server
docker exec -it name_container bash
```

## Inside image

```
mongosh
```

## Atraer un puerto por ssh de un contenedor docker corriendo en servidor

```
ssh -L 1234:127.0.0.1:27017 server-name
````
