# requirements file

Para construir un buen proyecto es necesario automatizar la descarga de
librerias que se van a utilizar.

Para ello se usa un fichero `requirements.txtp`

## Simbolos permitidos

Normalmente el contenido el fichero sigue el siguiente patron:

```txt
<paqute><simbolo><version>
```

Por ejemplo algo valido seria `numpy==1.26.0`

Los simbolos permitidos son:

- `==`: estricto
- `~=`: Primer digito igual
- `<` `>`: trivial
- `<=` `>=`: trivial
