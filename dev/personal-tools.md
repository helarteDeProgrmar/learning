# Herramientas interesantes

- `xournalpp`: pizarra open sources

## i3

`i3` es un gestor de ventanas, sustituye a GNOME en otras palabras.
Es minimalista y muy configurable.

Para sobrevivir aqui estan los comando basicos:

| Acción                            | Comando (por defecto, usando `$mod = Super/Windows`)   |
| --------------------------------- | ------------------------------------------------------ |
| **Abrir terminal**                | `Mod+Enter` (abre Alacritty o el terminal configurado) |
| **Cerrar ventana**                | `Mod+Shift+Q`                                          |
| **Abrir menú de aplicaciones**    | `Mod+D` (usa `dmenu` o `rofi`)                         |
| **Moverse entre ventanas**        | `Mod+H / J / K / L` (izq/abajo/arriba/derecha)         |
| **Mover ventana activa**          | `Mod+Shift+H / J / K / L`                              |
| **Dividir horizontal / vertical** | `Mod+V` (vertical) / `Mod+B` (horizontal)              |
| **Pantalla completa**             | `Mod+F`                                                |
| **Alternar modo flotante**        | `Mod+Shift+Space`                                      |
| **Recargar configuración**        | `Mod+Shift+R`                                          |
| **Cerrar sesión de i3**           | `Mod+Shift+E`                                          |

### Brillo

El mayor problema que he tenido hasta el momento es el brillo,
para cambiarlo:

```bash
sudo apt install brightnessctl
brightnessctl set +10% # subir
brightnessctl set 10% # exacto
brightnessctl set 10%- # bajar
```

En la configuracion de i3 las teclas son las siguientes:

| Nombre    | Significado                  |
| --------- | ---------------------------- |
| `Mod1`    | Tecla Alt                    |
| `Mod4`    | Tecla Super (usualmente Win) |
| `Control` | Tecla Ctrl                   |
| `Shift`   | Tecla Shift                  |
