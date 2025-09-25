# 🔍 Expresiones Regulares (Regex)

Una **expresión regular** es un patrón que describe conjuntos de cadenas de
texto.
A diferencia de los **globs**, las regex no están limitadas a nombres de
archivo: sirven para buscar, validar o reemplazar texto en cualquier contexto.

---

## 📌 Componentes básicos

| Regex    | Significado                                             | Ejemplo     | Coincide             | No coincide  |
| -------- | ------------------------------------------------------- | ----------- | -------------------- | ------------ |
| `.`      | Cualquier carácter (excepto salto de línea por defecto) | `a.c`       | `abc`, `axc`         | `ac`         |
| `*`      | Cero o más repeticiones del patrón anterior             | `ab*c`      | `ac`, `abc`, `abbbc` | `abbx`       |
| `+`      | Una o más repeticiones                                  | `ab+c`      | `abc`, `abbbc`       | `ac`         |
| `?`      | Cero o una repetición (opcional)                        | `colou?r`   | `color`, `colour`    | `colouur`    |
| `[...]`  | Conjunto de caracteres                                  | `[abc]`     | `a`, `b`, `c`        | `d`          |
| `[^...]` | Negación del conjunto                                   | `[^0-9]`    | `a`, `!`             | `1`, `5`     |
| `{n}`    | Exactamente `n` repeticiones                            | `a{3}`      | `aaa`                | `aa`         |
| `{n,}`   | `n` o más repeticiones                                  | `a{2,}`     | `aa`, `aaa`, `aaaa`  | `a`          |
| `{n,m}`  | Entre `n` y `m` repeticiones                            | `a{2,4}`    | `aa`, `aaa`, `aaaa`  | `a`, `aaaaa` |
| `^`      | Inicio de línea                                         | `^foo`      | `foobar`             | `barfoo`     |
| `$`      | Fin de línea                                            | `bar$`      | `foobar`             | `barfoo`     |
| `\d`     | Dígito (`[0-9]`)                                        | `\d\d`      | `42`                 | `ab`         |
| `\w`     | Carácter alfanumérico o `_`                             | `\w+`       | `hello_123`          | `!!!`        |
| `\s`     | Espacio en blanco                                       | `a\sb`      | `a b`                | `ab`         |
| `( )`    | Agrupación                                              | `(ha)+`     | `ha`, `hahaha`       | `h`          |

---

## 📚 Ejemplos prácticos

1. **Validar email (simplificado):**

```regex
^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$
```

   * `^` inicio de cadena
   * `[A-Za-z0-9._%+-]+` nombre de usuario
   * `@` literal
   * `[A-Za-z0-9.-]+` dominio
   * `\.` punto literal
   * `[A-Za-z]{2,}` extensión (al menos 2 letras)
   * `$` fin de cadena

2. **Números de teléfono simples (ej: `+34 600123456`):**

```regex
^\+?\d{1,3}\s?\d{6,12}$
```

3. **Extraer hashtags de un texto:**

```regex
#\w+
```

Coincide con `#coding`, `#2025`, `#hello_world`.
