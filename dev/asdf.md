# asdf

**asdf** es un tool version manager.
Para mas info sobre los comandos [docs](ttps://asdf-vm.com/manage/commands.html)

## Instalacion

Ejecutar el comando:

```bash
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.0
```

Añadir al fichero `.zshrc`:

```bash
. "$HOME/.asdf/asdf.sh"
. "$HOME/.asdf/completions/asdf.bash"
```

## Secuencia natural de asdf

```bash
asdf plugin list # ver plugins instalados (ej. elixir, erlang)
asdf list elixir # ver versiones instaladas de plugin (ej. v.1.18-otp-28)
asdf plugin add elixir # puedes tener versiones de elixir (descargar elixir)
asdf plugin add <name> [git-url] # puedes tener versiones de elixir (descargar desde git)
asdf list-all elixir # lista las versiones disponibles (no instaladas tambien)
asdf install elixir <version> # instala la version
asdf global elixir <version> # usa la version de forma predeterminada
asdf local elixir <version> # usa la version en el directorio actual
asdf current elixir # saber que version se esta utilizando
```

```bash
asdf current # ver las versiones para el directoria actual
```

## Ficheros donde guarda la informacion de version

- General: `~/.tool_versions`
- Especifica: En cada directorio fichero anterior

## PROBLEMAS FRECUENTES

Siempre que tengas un error revisa que tengas las dependencias correctas, tanto
la instalacion de `asdf`, como para cualquier plugin. (ej. erlang da muchos
problemas)
