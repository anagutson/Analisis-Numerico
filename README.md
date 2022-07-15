# Analisis Numerico 75.12

# Interpolación por Spline

## Objetivo

El objetivo del punto en cuestión es proveer una forma genérica de construir un spline cúbico de frontera ligada a partir de los datos iniciales, y luego aplicar lo concluído a los datos dados en el enunciado.

Para realizar esto, primero se plantea el problema de interpolación con Spline de frontera ligada.

Luego, a partir de las ecuaciones que conforman las condiciones necesarias para la construcción del Spline, se llega a un sistema de ecuaciones. A partir de la resolución del mismo, se podrá finalmente construir el Spline buscado.

En la resolución del punto además se brindan dos implementaciones que, a partir de datos iniciales, construyen el Spline Cúbico.

Por último, todo lo concluído se aplica a los datos iniciales brindados por el enunciado, obteniendo $3$ splines, los cuales son graficados para poder apreciar la aproximación resultante.

## Planteo

Para poder construir un Spline Cúbico de frontera ligada, se requiere conocer los siguientes valores:

$\quad \bullet \quad$ Puntos a interpolar (coordenadas $x$ e $y$).

$\quad \quad \rightarrow \quad$ siendo el conjunto de $x$ escrito con la notación $a = x_0 < x_1< \dots < x_n = b.$

$\quad \bullet \quad$ Valor de la derivada primera de la función en los extremos de la misma. 

Luego, se plantean $6$ condiciones que deben cumplirse para la construcción del polinomio interpolador.

Cada Spline estará conformado por polinomios cúbicos $S_j(x)$, definidos en el subintervalo $[x_j, x_{j+1}]$ para cada $j = 0, 1, \dots, n-1$, de la forma
$S_j(x) = a_j + b_j (x-x_j) + c_j (x-x_j)^2 + d_j (x-x_j)^3$.


## Desarrollo de las ecuaciones

Se realiza un análisis del problema a partir de las ecuaciones escritas en el ítem anterior, tal que se finaliza con un sistema lineal de ecuaciones:

$2(x_1-x_0) c_0 +(x_1-x_0)c_1 = 3\frac{a_1-a_0}{x_1-x_0} - 3f'(x_0)$\
$(x_1-x_0) c_0 + 2[(x_1-x_0) + (x_2-x_1)] c_1 + (x_2-x_1) c_2 = 3\frac{a_2-a_1}{x_2-x_1} - 3\frac{a_1-a_0}{x_1-x_0}$\
$(x_2-x_1) c_1 + 2[(x_2-x_1) + (x_3-x_2)] c_2 + (x_3-x_2)c_3 = 3\frac{a_3-a_2}{x_3-x_2} - 3\frac{a_2-a_1}{x_2-x_1}$\
$\quad\dots$\
$(x_{n-1}-x_{n-2}) c_{n-2} + 2[(x_{n-1}-x_{n-2}) + (x_n-x_{n-1})] c_{n-1} + (x_n-x_{n-1})c_n = 3\frac{a_n-a_{n-1}}{x_n-x_{n-1}} - 3\frac{a_{n-1}-a_{n-2}}{x_{n-1}-x_{n-2}}$\
$(x_n-x_{n-1}) c_{n-1} + 2(x_n-x_{n-1}) c_n = 3f'(x_n) - 3\frac{a_n-a_{n-1}}{x_n-x_{n-1}}$

Al resolver dicho sistema lineal, se obtendran los coeficientes $\{c_j\}^n_{j = 0}$ que se utilizarán en la construcción del spline.

# Código

Se realizan dos implementaciones para poder construir un Spline a partir de los datos iniciales.

La primera forma es realizada a partir de lo concluído previamente.

$\quad \bullet \quad$ Con los datos iniciales se arman las matrices $A$ y $b$.\
$\quad \bullet \quad$ Luego se resuelve el sistema mediante la factorización $LU$, obteniendo los coeficientes $\{c_j\}^n_{j = 0}$.

$\quad \bullet \quad$ Se calculan los coeficientes restantes, sabiendo además que los coeficientes $\{a_j\}^n_{j = 0}$ corresponden a la coordenada $y$ de cada nodo:

$\quad\quad - \quad$ Los $b_j$ se calculan como:
$$b_j = \frac{a_{j+1}-a_j}{x_{j+1}-x_j} - \frac{(x_{j+1}-x_j)(2c_j + c_{j+1})}{3}$$

$\quad\quad - \quad$ Los $d_j$ se calculan a partir de
$$d_j = \frac{(c_{j+1} - c_j)}{3(x_{j+1}-x_j)}$$

La segunda forma es una implementación realizada a partir de lo explicado en la bibliografía de la materia.


## Bibliografía

$\quad \bullet \quad$ Análisis Numérico, 10a edición - Burden - Faires.


____________________________________________

Trabajo Práctico elaborado en el primer cuatrimestre de 2022.
