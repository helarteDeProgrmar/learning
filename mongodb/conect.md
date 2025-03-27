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
