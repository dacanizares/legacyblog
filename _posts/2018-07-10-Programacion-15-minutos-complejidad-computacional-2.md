---
published: true
title: Programación en 15 minutos - Complejidad Computacional (Parte 2)
layout: post
tsocurl: http://thescienceofcode.azurewebsites.net/Articles/Show/5b4575cf407d6f33cc0e9d88
---
![Programación en 15 minutos - Complejidad Computacional 2]({{ site.baseurl }}/images/complexity-2.jpg)

{:.img-footer}
[Photo under Public Domain](https://unsplash.com/photos/N2HtDFA-AgM){:target='_blank'}

En este capítulo nos valdremos de un problema clásico de la computación para introducirnos de lleno en el análisis de algoritmos.

<!--more-->

# Órdenes de crecimiento

Para hablar de **Complejidad Computacional**, es necesario comprender el concepto de **órdenes de crecimiento**.

Los órdenes de crecimiento no son más que funciones matemáticas que utilizamos para representar cómo se comporta un algoritmo a medida que el tamaño de la entrada aumenta, en otras palabras, *es la forma en que medimos la cantidad aproximada de pasos que un algoritmo ejecuta de acuerdo a una entrada recibida*.

## Búsquedas en arreglos

Nos valdremos de uno de los problemas clásicos de la computación para explorar un poco de qué va esto de la **Complejidad Computacional**.

Supongamos que tenemos un arreglo **v** con **n** elementos ordenados de menor a mayor. ¿Cómo podríamos determinar si un elemento **x** está o no en dicho arreglo?

Para efectos de facilidad en la explicación, consideremos que **v** contiene los siguientes elementos:

```python
# v: vector
# n: tamaño del vector  (para nuestro caso sería 7)
v = [1, 2, 3, 5, 7, 9, 10]
n = len(v)
```

### Aproximación inicial

Un algoritmo sencillo que podríamos utilizar podría ser iterar sobre cada uno de los elementos mirando si alguno de ellos es **x**, este proceso es conocido como **Búsqueda Lineal**.

```python
def existe(v, x):
    for numero in v:
        if numero == x:
            return True
    return False
```

Ahora bien, analicemos cuántos pasos debe realizar el algoritmo en **el peor de los casos** (*en análisis de complejidad, por lo general tratamos de tomar el caso más difícil de modo que tengamos garantías sobre el comportamiento del algoritmo*).

En nuestro ejemplo, si nos piden buscar **x=10** deberíamos recorrer todo el arreglo antes de saber que existe el elemento, es decir:

* Nos ubicamos en el primer elemento del arreglo (**v[0]**) que contiene el valor **1**. Como no es **10** continuamos con la siguiente posición.

* Revisamos la segunda posición (**v[1]**) que contiene el valor **2**. Como no es **10** continuamos con la siguiente posición.

* Y así sucesivamente hasta que en la última posición encontramos el número **10**.

En otras palabras, si tenemos 7 elementos en el arreglo, en **el peor caso** debemos revisar los 7 elementos antes de estar seguros si el número está o no presente. Si tuvieramos 100 elementos, habría que revisar los 100 elementos. Si fueran **n** los elementos, habría que revisar entonces **n** elementos.

> Una **Búsqueda Lineal** para un arreglo de **n** elementos tarda en el peor de los casos **n** iteraciones para encontrar la respuesta.

### Mejorando el algoritmo

Ya que sabemos que los elementos están ordenados de mayor a menor, podríamos intentar algo más inteligente:

* Ubicarnos en el valor que se encuentra en la mitad del arreglo, en este caso sería **5**. Recordemos que estamos buscando el número **10**, luego, sabemos que hay que seguir buscando en los valores que están a la derecha del **5** (ya que a la izquierda son menores), de modo que podemos descartar de golpe la mitad del arreglo.

    ```python
    v = [1, 2, 3, 5, 7, 9, 10]
                  ^
    ```

* Repetimos el proceso con los elementos que quedan en el arreglo: ubicamos la mitad y miramos si el dato está a la izquierda o la derecha hasta que lo encontremos (o hasta que descartemos todos los elementos).

    ```python
    v = [x, x, x, x, 7, 9, 10]
                        ^

    v = [x, x, x, x, x, x, 10]
                            ^
                        ¡Encontrado!
    ```

Esta segunda aproximación se conoce como **Búsqueda Binaria**. A continuación les dejo un video de CS50 de Standford en el que explican con mayor claridad ambos tipos de búsqueda.

[![Búsqueda binaria vs búsqueda lineal](https://img.youtube.com/vi/y62zj9ozPOM/0.jpg)](https://youtu.be/y62zj9ozPOM?t=1316)

Luego de ver el video, sabemos que la cantidad de pasos para la **Búsqueda Binaria** es de **log2(n)**. De forma general, podemos decir que en un algoritmo en el que a cada paso descartamos la mitad de los datos disponibles, tendremos que  iterar como máximo **log2(n)**  veces en **el peor de los casos** para hallar la respuesta.

> Una **Búsqueda Binaria** para un arreglo de **n** elementos tarda en el peor de los casos **log2(n)** iteraciones para encontrar la respuesta.

El siguiente es el código que implementa una **Búsqueda Binaria**:

```python
# v: arreglo con n elementos
# x: elemento a buscar
# izq: posición más a la izquierda donde estamos buscando
# der: posición más a la derecha donde estamos buscando
def binaria(v, x, izq, der):
    # Si esto ocurre no hemos encontrado el elemento
    # y ya se ha revisado todo el arreglo
    if izq > der:
        return False

    # Calculamos la mitad
    mid = (izq + der) / 2
    # Miramos si lo encontramos
    if v[mid] == x:
        return True
    # O si buscamos por la derecha
    if x > v[mid]:
        # Descartamos todo el lado izquierdo
        # haciendo que izq sea mid + 1
        return binaria(v, x, mid + 1, der)
    # O si no por la izquierda
    else:
        # Descartamos todo el lado derecho
        # haciendo que der sea mid - 1
        return binaria(v, x, izq, mid - 1)
```

## Análisis de los resultados

| Tamaño de la entrada (n) | Búsqueda Lineal  | Búsqueda Binaria   |
|---------                 |---------         |---------           |
|10                        | 10               | 4                  |
|1,000                     | 1,000            | 10                 |
|100,000                   | 100,000          | 17                 |
|1,000,000                 | 1,000,000        | 20                 |
|10,000,000                | 10,000,000       | 24                 |

Como podemos ver, para una cantidad considerable de datos, la diferencia entre ambos algoritmos es gigantesca, pasado de 10 millones de pasos en la **Búsqueda Lineal** a tan sólo 24 pasos en la **Búsqueda Binaria**.

## Notación Big O

Los programadores suelen utilizar la **notación big-o** (*pronunciado big-ou*) para indicar el órden de crecimiento (o complejidad) de un algoritmo. Aunque en capítulos posteriores veremos más detalles, de momento nos bastará con saber lo más general.

* Un algoritmo que para una entrada de tamaño **n** toma aproximadamente **n** pasos en encontrar la respuesta lo representamos como **O(n)** y podemos decir que tiene una **Complejidad Lineal**.

* Un algoritmo que para una entrada de tamaño **n** toma aproximadamente **log(n)** pasos en encontrar la respuesta lo representamos como **O(log(n))** y podemos decir que tiene una **Complejidad Logarítimica**.

En general, un algoritmo de **Complejidad Logarítmica** es preferible, dado que su desempeño es superior. Sin embargo, no siempre es posible encontrar un algoritmo de este estilo.

Por su parte, un algoritmo de **Complejidad Lineal** tendrá un buen desempeño, inclusive en aplicaciones de tiempo real como videojuegos, siempre y cuando el tamaño de la entrada sea moderado.

> En general, un algoritmo que para una entrada de tamaño **n** toma aproximadamente **f(n)** pasos en encontrar la respuesta, donde **f(n)** es una función matemática cualquiera,  lo representamos como **O(f(n))**.

En el próximo capítulo veremos cuáles son las principales funciones que nos podemos encontrar como programadores.

¡Hasta la próxima!
