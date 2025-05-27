# Borrar ficheros del repositorio

## Borrar ficheros que no estan traqueados o no pertercen a la historia

```bash
git clean -fd # borrar todo lo no traqueado
git clean -fdx # !!!! tambien los fichero ignorados por git
git clean -nd # revisar que ficheros se eliminan
```

## No preguntar por ficheros antes no ignorados

Puede darse el caso en que a veces no se quiera seguir subiendo un
fichero a la historia pero su antigua version no te importa. Entonces
usa:

`git rm --cached ruta/al/fichero && git commit -m "stop tracking"`
