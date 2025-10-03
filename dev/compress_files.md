# Comprimir descomprimir ficheros linux

## zip

Lo primero es comprobar la instalacion: `zip --version`
```bash
zip -r archivo.zip carpeta/
zip archivo.zip archivo1.txt archivo2.txt
zip archivo.zip * -x "*.log"
```
Descomprimir con: `unzip archivo.zip -d direcction/to/descompress`

## tar

La estructura basica es: `tar [opciones] archivo.tar archivos_o_directorios`

Las opciones mas tipicas:

| Opción | Significado                                       |
| ------ | ------------------------------------------------- |
| `-c`   | **Crear** un nuevo archivo tar (create)           |
| `-x`   | **Extraer** archivos de un tar (extract)          |
| `-t`   | **Listar** el contenido de un tar (list)          |
| `-v`   | Modo **verbose**, muestra los archivos procesados |
| `-f`   | Especifica el **nombre del archivo tar**          |
| `-z`   | Comprimir/descomprimir con **gzip** (`.tar.gz`)   |
| `-j`   | Comprimir/descomprimir con **bzip2** (`.tar.bz2`) |

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
