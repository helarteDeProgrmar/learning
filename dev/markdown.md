# Markdowm

En este documento se intentara recoger lo basico de markdown.

Un interesantisimo enlace que da la vida [detexify](https://detexify.kirelabs.org/classify.html)

## Matematicas

En caso de querer algo mas concreto: [manual de latex](https://manualdelatex.com/tutoriales/ecuaciones)

### Operaciones elementales

$$ suma: a + b $$
$$ producto: a * b $$
$$ division: a / b $$
$$ fraccion: \frac{a}{b} $$
$$ potencia: a ^ b $$
$$ potencia larga: a ^ {b - c} $$

### Funciones


### Conbinatoria

$$f\left(k\right) = \binom{n}{k} p^k\left(1-p\right)^{n-k}$$ 

### Diagramas

### General

## Titulos, negrita, cursiva

**negrita**
*cursiva*
Trivial, leete el documento en plano

## Imagenes

`knitr::include_graphics()`
`knitr::include_graphics("02_libro2.png")`

Parametros:

```md
-fig.asp
-fig.width
-fig.height
-fig.align
-out.width
```

## Enlaces

[nombre del enlace](https://www.google.com) es un enlace a google

## Hacer pdf

Instalar pandoc y tex:

```bash
sudo dnf install pandoc
sudo dnf install texlive-scheme-full
sudo dnf install texlive-xetex # Si no viene en el full
```

Despues de la prueba resulta que no es muy util, pero teniendo latex
para crear pdf nos bastara eso.
