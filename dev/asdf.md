# asdf

**asdf** es un ool version manager.
Para mas info sobre los comandos [docs](ttps://asdf-vm.com/manage/commands.html)

## Secuencia natural de asdf

```bash
asdf plugin list # ver plugins instalados
asdf plugin add elixir # puedes tener versiones de elixir
asdf plugin add <name> [git-url] # puedes tener versiones de elixir
asdf list-all elixir # lista las versiones disponibles
asdf install elixir <version> # instal la version
asdf global elixir <version> # usa la version de forma predeterminada
asdf local elixir <version> # usa la version en el directorio actual
```


```bash
asdf current # ver las versiones para el directoria actual
```

## Ficheros donde guarda la informacion de version

- General: `~/.tool_versions`
- Especifica: En cada directorio fichero anterior
