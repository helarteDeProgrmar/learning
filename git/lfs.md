# Git LFS

Esta herramienta es la solucion para compartir archivos del tipo
`no-texto-plano` de forma remota.

Esta herramienta trabaja apartando dentro de los repos una parte del directorio
`.git` para este tipo de archivos. Se guardan las versiones una por una dentro
de una carpeta especial.

## Basic

### Instalacion

```bash
sudo apt install git-lfs # para ubuntu
```

### Inicializar un repo

```bash
git init
git lfs install
```

### Trackear los tipos de ficheros deseados

```bash
git lfs track "*.pdf"
git lfs track "*.png"
git lfs track "*.mp4"
```

```bash
git add .gitattributes
git commit -m "Configurar Git LFS para PDF, PNG, MP4"
```

### Archivos gestionados por lfs

```bash
git lfs ls-files
```

### Limpiar versiones antiguas

```bash
git lfs prune
```

### Mas comandos utiles

| Comando                                    | Qué hace                                                 |
| ------------------------------------------ | -------------------------------------------------------- |
| `git lfs env`                              | Muestra configuración y rutas de LFS                     |
| `git lfs status`                           | Muestra qué archivos están pendientes de subir o cambiar |
| `git lfs fetch --all`                      | Descarga todos los objetos LFS del remoto                |
| `git lfs migrate import --include="*.pdf"` | Convierte archivos existentes del repo normal a LFS      |
