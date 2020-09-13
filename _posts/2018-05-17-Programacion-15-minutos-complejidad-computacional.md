---
published: true
title: Programación en 15 minutos - Complejidad Computacional (Parte 1)
layout: post
tsocurl: http://thescienceofcode.azurewebsites.net/Articles/Show/5afe49c93e671569ac7d12fe
---
![Programación en 15 minutos - Complejidad Computacional]({{ site.baseurl }}/images/complexity-1.jpg)

{:.img-footer}
[Photo under Public Domain](https://unsplash.com/photos/Q1p7bh3SHj8){:target='_blank'}

En 1993 John Carmack y su equipo en **id software** publicaron **Doom**, el juego que cambió para siempre la computación. En los equipos de aquella época, con todas sus limitaciones técnicas y su reducida capacidad de cómputo, Carmack logró renderizar increíbles gráficos tridimensionales en tiempo real. El secreto para conseguirlo fue un intrincado algoritmo que de forma eficiente permitía representar y dibujar los entornos 3D. Para comprender qué hace a un algoritmo **eficiente**, en esta serie de **Programación en 15 minutos** nos introduciremos a la **Complejidad Computacional**.
<!--more-->

# Ejemplo práctico

Una de las herramientas más útiles que tiene un programador es el análisis de la complejidad de un algoritmo. Una solución computacional poco eficiente hará que una calculadora común o incluso una persona pueda ganarle a una supercomputadora realizando una operación.

Por ejemplo, comparemos dos algoritmos para computar la multiplicación entre dos números *a* y *b*.

## Algoritmo 1

La multiplicacion *a* por *b* es igual a sumar *b*
veces *a*.

```python
def algoritmo_1(a, b):
    resultado =  0
    while b > 0:
        resultado += a
        b -= 1
    return resultado
```

## Algoritmo 2

Utilizaremos el operador que tienen los lenguajes de programación para este propósito.

```python
def algoritmo_2(a, b):
    return a * b
```

## Resultados

Para la prueba hemos puesto a correr ambos algoritmos en un procesador *i7*, poniendo un valor constante para *a* y modificando el valor *b* (columna entrada) obteniendo los siguientes resultados al medir el tiempo que se demoran en llegar a la respuesta:

| Entrada            | Algoritmo 1 | Algoritmo 2 |
| ------------------ | ----------- | ----------- |
| 1 millón           | 0.092 seg   | 0.0 seg     |
| 10 millones        | 0.188 seg   | 0.0 seg     |
| 100 millones       | 0.272 seg   | 0.0 seg     |
| 1.000 millones     | 0.348 seg   | 0.0 seg     |
| 10.000 millones    | 0.488 seg   | 0.0 seg     |
| 100.000 millones   | 0.530 seg   | 0.0 seg     |
| 1 billón           | 0.667 seg   | 0.0 seg     |
| 10 billones        | 0.733 seg   | 0.0 seg     |
| 100 billones       | 0.801 seg   | 0.0 seg     |
| **Total**          | **4.1 segs**    | **< 0.001 seg** |

## Análisis

Como podemos ver, a medida que aumenta el tamaño de la entrada, se hace mayor la diferencia entre los tiempos de respuesta de los algoritmos. Quizá para datos pequeños no sea muy notable, pero a medida que aumenta la complejidad de la operación, cada vez es más evidente que el *Algoritmo 1* es mucho **menos eficiente** que el *Algoritmo 2*.

Para nuestro caso, el tamaño de la entrada es un simple número, pero si estuvieramos hablando en términos reales podríamos estar refiriéndonos, por citar un par de ejemplos, a:

* **El número de usuarios conectados a una aplicación web**: Quizá una aplicación poco eficiente funcione bien con cientos de usuarios concurrentes, pero a medida que aumente esa cifra a miles o incluso millones de usuarios, el sistema terminará por colapsar.

* **Cálculos de efectos visuales de un juego**: Para construir un juego con gráficos simples es posible que un algoritmo poco eficiente sea suficiente como para pintar las imagenes en la pantalla y que todo se vea relativamente bien, pero si queremos calcular sombras e iluminación en tiempo real en un entorno 3D, una solución poco elaborada hará que toda la visalización cargue lento, que no se aprevechen bien todos los recursos de la máquina y que al final la experiencia termine yéndose al traste.

Así pues, tanto si queremos crear experiencias de tiempo real complejas, como si queremos que nuestras aplicaciones escalen correctamente, es muy importante conocer herramientas que nos permitan analizar el comportamiento de los algoritmos. Una de esas herramientas es la **Complejidad Computacional** y durante las próximas entregas aprenderemos de qué va todo esto. ¡Hasta la próxima!
