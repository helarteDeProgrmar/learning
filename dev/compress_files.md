# Comprimir descomprimir ficheros linux

## zip

Lo primero es comprobar la instalacion: `zip --version`
Comprimir con: `zip -r directory directory.zip`
Descomprimir con: `unzip archivo.zip -d direcction/to/descompress`

## rar

**Isntalar rar**

Bastante criminal la descarga que he hecho, pero
funciona:

```txt
cd /tmp
curl -O https://www.rarlab.com/rar/rarlinux-x64-621.tar.gz
```


```txt
tar -xzf rarlinux-x64-621.tar.gz
cd rar
sudo install -v -m755 rar unrar /usr/local/bin
```

**Comprimir un archivo o carpeta**

```txt
rar a archivo.rar archivo.txt
rar a archivo.rar carpeta/
```

**Usar la unrar:**

`unrar x archivo.rar /ruta/al/final/dir`

la opciones x es para mantaener la estructura de directorios

Con la opcion `e` se cogen todos los archivos sin estructura
