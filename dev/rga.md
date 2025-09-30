# Busqueda en sistemas linux

## find vs grep

### Idea intuitiva

- `find` → “¿Dónde está este archivo/carpeta en el sistema?”, archivos
- `grep` → “¿Dónde aparece este texto dentro de archivos?”, texto

### find

```bash
# 1. Buscar un archivo por nombre exacto
find /ruta -type f -name "archivo.txt"

# 2. Buscar por coincidencia parcial (insensible a mayúsculas)
find /ruta -type f -iname "*parte*nombre*"

# 3. Buscar directorios
find /ruta -type d -name "backup"

# 4. Buscar por extensión
find /ruta -type f -name "*.log"

# 5. Buscar por tamaño
find /ruta -type f -size +100M    # mayor de 100 MB
find /ruta -type f -size -10k     # menor de 10 KB

# 6. Buscar por fecha
find /ruta -type f -mtime -1      # modificados en las últimas 24h
find /ruta -type f -ctime -7      # cambiados en los últimos 7 días

# 7. Buscar por permisos o propietario
find /ruta -type f -perm 644
find /ruta -type f -user juan
find /ruta -type f -group staff

# 8. Eliminar archivos vacíos
find /ruta -type f -empty -delete
```

### grep

```bash
# 1. Buscar texto exacto
grep "ERROR" archivo.log

# 2. Buscar texto ignorando mayúsculas/minúsculas
grep -i "error" archivo.log

# 3. Buscar en varios archivos a la vez
grep "ERROR" *.log

# 4. Mostrar número de línea donde aparece
grep -n "ERROR" archivo.log

# 5. Mostrar solo el nombre del archivo donde aparece
grep -l "ERROR" *.log

# 6. Mostrar coincidencias en color
grep --color=auto "ERROR" archivo.log

# 7. Buscar recursivamente en un árbol de directorios
grep -r "TODO" /ruta/codigo/

# 8. Excluir líneas que coincidan
grep -v "DEBUG" archivo.log
```

## rg

Sirve para directorios o proyectos mucho mas grandes. Es una alternativa a
`grep`

## rga

Para buscar en distintos ficheros igual que si fuese rg
podemos usar `rga`

### Instalacion

La instalacion es bastante interesante:

1. Descargamos en binario
2. Guardamos en opt
3. Creamos un link simbolico a `/usr/bin`

### Uso

```bash
# 1. Buscar una palabra en el directorio actual (recursivo por defecto)
rga "ERROR"

# 2. Buscar ignorando mayúsculas/minúsculas
rga -i "error"

# 3. Mostrar el número de línea
rga -n "usuario"

# 4. Solo mostrar el nombre de los archivos que coinciden
rga -l "palabra"

# 5. Buscar varias palabras (expresión regular)
rga "ERROR|FATAL"

# 6. Excluir un directorio (ej: node_modules)
rga "TODO" --ignore-dir node_modules

# 7. Limitar el tipo de archivo (ej: solo PDFs)
rga "informe" --type pdf

# 8. Forzar a buscar también en archivos ignorados por .gitignore
rga -uu "token"

# 9. Buscar dentro de un ZIP o PDF directamente
rga "confidencial" archivo.zip
rga "contrato" archivo.pdf

# 10. Buscar y mostrar solo el nombre del archivo + línea encontrada
rga -Hn "clave"

# 11. Para estar seguro
rga --help
```
