# Latex

## Compilacion

```tex
\begin{verbatim}
$ pdflatex tfg_etsiinf_LuisAmigo
$ biber tfg_etsiinf_LuisAmigo
$ pdflatex tfg_etsiinf_LuisAmigo
$ pdflatex tfg_etsiinf_LuisAmigo
\end{verbatim}
```

## Listas

- `itemize`
- `enumerate`

## Tablas

- `tabular`:

```tex
\begin{tabular}{||l|c|r|p{15em}||}
  \hline
  \hline
  \textbf{Alimento} & \textbf{Categoría} & \textbf{Kcal/100gr} &
\textbf{Descripción}\\
  \hline
  \hline
  Manzana & Fruta & 52 & Es el fruto comestible de la especie Malus domestica,
el manzano común. Es una fruta pomácea de forma redonda y sabor muy dulce,
dependiendo de la variedad.\\
  \hline
  Repollo & Verdura & 19 & Es una planta comestible de la familia de las
Brasicáceas, y una herbácea bienal, cultivada como anual, cuyas hojas lisas
forman un característico cogollo compacto.\\
  \hline
  \hline
\end{tabular}
```

- `longtable`

## Referencias

- `label`: `\ref{ch:intro}`
- `ref`: `\ref{sec:latex}.`

```tex
En este sition saldra el numerito\footnote{y esto sera el pie de pagina}
```

## Textos

```tex
\textrm{}
\textbf{}
\emph{}
\textit{}
\texttt{}
\textsc{}
```

## Comillas

Las commillas se ecriben:

```tex
``comillas dobles''
`comillas simples'
con el paquete \url{csquotes} se puede: \enquote{texto}
```

## Alinear

- `\center`
- `\hfill`

## Figuras

```tex
\emph{here}, \emph{top} o \emph{bottom} con \verb|[h]|, \verb|[t]| o
\verb|[b]|.

\begin{figure}[h]
  \centering
  \includegraphics[width=0.33\linewidth]{portada/escudo_etsiinf}
  \caption{El escudo de la ETSIINF}
  \label{fig:escudo}
\end{figure}

O grafico en el centro...
\begin{center}
  \includegraphics[width=0.15\linewidth]{portada/escudo_upm}
\end{center}
```

## Maths

En general comenzar con `$$` o

```tex
\begin{center}
  \includegraphics[width=0.15\linewidth]{portada/escudo_upm}
\end{center}
```

Ver [este fichero](dev/docs/markdown.md) para mas...

## Codigo

```tex
\begin{lstlisting}[language=c]
#include <stdio.h>
// A simple Hello World
int main(){
  printf("Hello World!\n");
  return 0;
}
\end{lstlisting}

\begin{lstlisting}[language=c,style=nocolor]
#include <stdio.h>
// A simple Hello World
int main(){
  printf("Hello World!\n");
  return 0;
}
\end{lstlisting}
```

Si quieres en una linea: `\lstinline{main()}`

Y sin importar: `\texttt{verbatim} o el comando \verb|\verb|`

## Rellenar de cosas locas

- `\lipsum`
