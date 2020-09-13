---
published: true
title: Programación en 15 minutos - Complejidad Computacional (Parte 3)
layout: post
license: ccbysa
tsocurl: https://thescienceofcode.azurewebsites.net/Articles/Show/5bcb637b44064a607035298b
---
![Programación en 15 minutos - Complejidad Computacional 3]({{ site.baseurl }}/images/complexity-3.jpg)

{:.img-footer}
[Photo under Public Domain](https://unsplash.com/photos/E0AHdsENmDg){:target='_blank'}

En este capítulo exploraremos las principales funciones de crecimiento que podemos encontrarnos en nuestra carrera como programadores.

<!--more-->

> Esta parte será un poco más extensa de lo normal, pero prefiero no dividirlo en dos partes, para no romper con la estructura lógica que agrupa los conceptos que hoy vamos a aprender. ¿Listos? ¡Vamos!

# Órdenes de crecimiento más comunes

Recordemos que la **Notación Big O** es una herramienta que nos permite representar los órdenes de crecimiento de nuestros algoritmos, siendo estos *la forma en que medimos la cantidad aproximada de pasos que un algoritmo ejecuta de acuerdo a una entrada recibida*

Como programadores lo más común es encontrarse con alguno de los siguientes órdenes de crecimiento:

## Crecimiento constante

> Cuando un algoritmo puede dar la respuesta utilizando la misma cantidad de pasos independiente del tamaño de la entrada, decimos que tiene una complejidad constante, que está representada por **O(1)**

En general, son problemas solucionables mediante una única instrucción o mediante operaciones matemáticas. Por ejemplo:

* Calcular la sumatoria de los primeros **n** enteros usando la fórmula **n (n + 1) / 2**.

  ``` python  
  def sumatoria_hasta_n_tiempo_constante(n):
      # Simplemente aplicamos la operación matemática
      # correspondiente
      return n * (n + 1) / 2
  ```

* Encontrar el elemento en una posición **x** de un vector **v** (Sería simplemente acceder **v[x]**, lo que se consigue con vector en tiempo constante -en otras estructuras de datos como los mapas este tiempo puede variar).

   ``` python  
  def obtener_posicion_i_del_vector_v(v, i):
      return v[i]
  ```
  

* Este problema de Code Forces [Theatre Square](https://codeforces.com/problemset/problem/1/A){:target='_blank'}

Este tipo de soluciones son deseables ya que en términos generales podemos decir que son **algoritmos óptimos**, que escalan bien con el tamaño de la entrada y que normalmente tienen muy buen desempeño, es decir, que son muy rápidos.

## Crecimiento logarítmico

| ![Binaria](https://theproductiveprogrammer.blog/013/binary-search.png) |
| :--: |
| *Imagen de [Top Coder](https://dacanizares.github.io/images/binary-search.png){:target='_blank'}. Usada sólo con fines educativos.*  |

> Cuando un algoritmo en cada iteración descarta la mitad, un tercio o en general una fraccion de las posibles soluciones, decimos que tiene una complejidad logarítmica, que está representada por **O(log_b(n))**.

Recordemos la explicación de la búsqueda binaria del capítulo anterior, en la que en cada paso el algoritmo **descartaba la mitad de los datos de un directorio**, de manera que el programa podía llegar rápidamente a la respuesta.

* **log(n)**: si no se especifica la base, los programadores consideramos que la base del logarítmo es 2, lo que quiere decir que en cada paso se descarta la mitad de las posibilidades. 

  * La solución más popular de este tipo es la **búsqueda binaria** (en el capítulo anterior está el código en Python), que puede usarse por ejemplo, en este problema de Code Forces: [Worms](https://codeforces.com/contest/474/problem/B){:target='_blank'}.

* Funciones de crecimiento con logarítmos de otras bases, si bien existen, no son tan comunes de encontrar en programación por lo que pasaremos de largo sobre ellos.

Este tipo de soluciones también escalan correctamente y por lo general tienen muy buen desempeño. Recordemos la tabla comparativa de la cantidad de pasos para encontrar un elemento en un arreglo usando búsquedas binaria y lineal:

| Tamaño de la entrada (n) | Búsqueda Lineal  | Búsqueda Binaria   |
|---------                 |---------         |---------           |
|10                        | 10               | 4                  |
|1,000                     | 1,000            | 10                 |
|100,000                   | 100,000          | 17                 |
|1,000,000                 | 1,000,000        | 20                 |
|10,000,000                | 10,000,000       | 24                 |

## Funciones de crecimiento lineal

> Cuando un algoritmo itera **n**, **2n**, **3n**, o en general **cn** (siendo **c** constante) sobre una entrada de tamaño **n** para obtener la respuesta, decimos que tiene una complejidad [lineal](https://es.wikipedia.org/wiki/Funci%C3%B3n_lineal){:target='_blank'}, que está representada por **O(n)**

Para que un algoritmo esté en esta categoría debe iterar una cantidad constante de veces sobre la entrada. Como veremos en el próximo capítulo, esto significa NO tener ciclos anidados. Por ejemplo:
  
  * Búsqueda lineal.

    ```python
    def buscar_x_en_vector(v, x):
        # Recorremos todo el arreglo una vez
        for numero in v:
            if numero == x:
                return True
        return False
    ```

  * Hallar el mayor elemento de un vector.

    ```python
    def mayor_valor_en_vector(v):
        # Iniciamos con el primer valor
        mayor = v[0]
        # Y recorremos el resto del arreglo una vez
        for i in range(1, len(v)):
            # Mirando si hay alguno mayor
            if v[i] > mayor:
                mayor = v[i]
        return mayor
    ```

  * Hallar la sumatoria de los primeros **n** enteros sumando *1 + 2 + 3 ... n* dentro de un ciclo. Este es el mismo problema que resolvimos en tiempo constante, sólo que ahora aplicando un algoritmo menos optimizado.

    ```python
    def sumatoria_hasta_n(n):
        # Iniciamos una variable para acumular la sumatoria       
        suma = 0
        # Y recorremos desde 1 hasta n
        for i in range(1, n + 1):
            # Sumando los numeros
            suma += i
        return suma
    ```

  * Este problema de Code Forces: [Police Recruits](https://codeforces.com/contest/427/problem/A){:target='_blank'}  

Este tipo de soluciones, en general, funcionan muy bien en aplicaciones de tiempo real (como los videojuegos), siempre y cuando el tamaño de la entrada no sea exageradamente grande (cientos de miles máximo). De igual forma, en otro tipo de aplicaciones, cuando los datos llegan a *millones*, el desempeño del algoritmo se ve afectado.

## Funciones de crecimiento polinomial

> Cuando un algoritmo itera **n²**, **n³** o en general **n^c** sobre una entrada de tamaño **n** para obtener la respuesta, decimos que tiene una complejidad polinomial, que está representada por **O(n^c)**

* **O(n²)**: Lo encontramos cuando tenemos que comparar cada uno de los datos de entrada con todos los demás que la conforman o cuando trabajamos con matrices (ya que usualmente son de tamaño **n x n**). Por ejemplo,

  | ![Bubble sort](https://upload.wikimedia.org/wikipedia/commons/archive/5/54/20140912160203%21Sorting_bubblesort_anim.gif) |
  | :--: | 
  | *Bubble Sort [Wikipedia CC-BY-SA](https://commons.wikimedia.org/wiki/File:Sorting_bubblesort_anim.gif){:target='_blank'}* |


    * Organizar un vector usando bubble sort, ya que debemos recorrer todos los elementos y comparar cada uno de ellos con el resto de elementos (**n x n = n²**). 

      ```python
      def organizar_vector_con_bubblesort(v):
          # Recorremos todos los valores
          for i in range(n):
              # Comparando cada uno de ellos 
              # con todos los demás
              for j in range(i + 1, n):
                # Si el primero es mayor
                if v[i] > v[j]:
                  # Los intercambiamos
                  v[i], v[j] = v[j], v[i]
          return suma
      ```

    * En general, operaciones con matrices, como multiplicar una matriz por un número (lo que equivale a multiplicar cada uno de los valores de la matriz por ese número):

      ```python
       def multiplicar_matriz_por_numero(m, c):
           # Recorremos todos los valores de la matriz
           for i in range(m):
               for j in range(len(m[i])):
                 # Y los multiplicamos por c
                 m[i][j] *= c
           # Como las matrices funcionan por referencia,
           # no es necesario retornar
       ```

    * Este problema de Code Forces [Toy Cars](https://codeforces.com/contest/545/problem/A)

En esta categoria, el número de pasos con respecto al tamaño de la entrada comienza a escalar a proporciones muy grandes, de forma que lo ideal es aplicar este tipo de algoritmos con cuidado, teniendo presente que el performance y la escalabilidad del sistema pueden verse afectados con entradas de mayor tamaño.

> Los siguientes son órdenes de crecimiento un poco más complejos, así que de momento sólo haremos una breve aproximación a ellos.

## Crecimiento pseudo-logarítmico

> Cuando un algoritmo realiza **n** veces un procediento de tiempo **logarítmico** para obtener la respuesta, decimos que tiene una complejidad pseudo-logarítmica, que está representada por **O(nlog(n))**

| ![Quicksort](https://upload.wikimedia.org/wikipedia/commons/6/6a/Sorting_quicksort_anim.gif) |
| :--: |
| *Quick sort [Wikipedia CC-BY-SA](https://en.wikipedia.org/wiki/Quicksort#/media/File:Sorting_quicksort_anim.gif){:target='_blank'}* |

* Algoritmos optimizados de ordenamiento como Merge Sort, Heap Sort o Quick Sort.

* En el problema [Worms](https://codeforces.com/contest/474/problem/B){:target='_blank'}, si tenemos en cuenta **toda** la entrada, estamos realizando **n** búsquedas binarias, una por cada caso de prueba. 

Este tipo de soluciones tiene un comportamiento relativamente similar, aunque menos óptimo que el de las funciones de crecimiento **lineal**.

## Crecimiento exponencial

> Cuando un algoritmo realiza **2^n**, **3^n** o en general **C^n** pasos para obtener la respuesta, decimos que tiene una complejidad exponencial, que está representada por **O(C^n)**

Por lo general esto se produce cuando en cada paso, en vez de reducirse la cantidad de respuestas posibles, se van duplicando, triplicando... es decir, lo contrario a una solución logarítmica, o también cuando probamos todas las posibles soluciones de un problema, que tiene muchas respuestas, para encontrar la mejor de ellas.

En esta categoría usualmente algoritmos con complejidad **O(n!)**, está resulta cuando necesitamos iterar sobre la forma de organizar una serie de n elementos.

| ![Brute force](https://upload.wikimedia.org/wikipedia/commons/2/2b/Bruteforce.gif) |
| :--: |
| Ejemplo gráfico de un algoritmo de fuerza bruta. [Wikipedia CC-BY-SA](https://es.m.wikipedia.org/wiki/Archivo:Bruteforce.gif)

* Generar todos los posibles subconjuntos de un conjunto con **n** elementos. Un conjunto tiene **2^n** subconjuntos, luego habría que iterar para generar cada uno de esos subconjuntos. Por ejemplo, supongamos el conjunto S = { A, B, C } que tiene **2^3** subconjuntos (8), podríamos representar con 0 si un elemento no está y con 1 en caso contrario y obtener algo más o menos así:

  | Iteración | Binario  | Subconjunto que representa |
  |:---------:|:--------:|:--------------------------:|
  | 1         | 000      | { }                        |        
  | 2         | 001      | { C }                      |          
  | 3         | 010      | { B }                      |          
  | 4         | 011      | { B, C }                   |             
  | 5         | 100      | { A }                      |          
  | 6         | 101      | { A, C }                   |             
  | 7         | 110      | { A, B }                   |             
  | 8         | 111      | { A, B, C }                |                  
  |           | ABC      |                            |

* Algoritmos de fuerza bruta, es decir, en los que se prueban todos los posibles caminos para ver cuál de ellos lleva a la respuesta correcta.

* Este problema de Code Forces: [Shower Line](https://codeforces.com/contest/431/problem/B){:target='_blank'} que está relacionado con encontrar la mejor forma de organizar una fila de personas. Una fila puede organizarse de **n!** formas diferentes.

  ```python  
  def pseudocodigo_de_showerline(v):
      respuesta = 0
      # Para cada posible orden de la fila
      for orden in posibles_ordenes(fila):
          # Calculamos la felicidad de ese órden específico
          felicidad = .. + .. + ..
          respuesta = max(respuesta, felicidad)
      return suma
  ```


Este tipo de respuestas son **relativamente** fáciles de encontrar y de programar, pero tienen graves problemas de desempeño ya que la cantidad de pasos para encontrar la respuesta crece muy rápidamente.

## Comparativo general

En la siguiente tabla podemos ver la cantidad de pasos que debería realizar un algoritmo de cada órden de crecimiento para dar la respuesta correcta a una entrada de tamaño **n**, en el peor de los casos:

|                 | 10   | 1,000          |100,000          | 1'000,000      |
|:----------------|:----:|:--------------:|:---------------:|:--------------:|
| **O(1)**        | 1    | 1              | 1               | 1              |
| **O(log(n))**   | 4    | 10             | 17              | 20             |
| **O(n)**        | 10   | 1,000          | 100,000         | 1,000,000      |
| **O(n log(n))** | 40   | 10,000         | 1,700,000       | 20'000,000     |
| **O(n²)**       | 100  | 1'000,000      | 10 mil millones | 10 billones    |
| **O(2^n)**      | 1024 | 1,071 x 10^310 | Desbordamiento  | Desbordamiento |



Como podemos ver, algunos valores escalan tan rápidamente que incluso en computadores modernos es imposible calcularlos. Así que la próxima vez, antes de sentarse a programar es bueno tener en consideranción todo lo que hemos aprendido sobre **Complejidad Computacional** para garantizar que nuestros algoritmos no sólo funcionan si no que lo hacen de forma eficiente.

## Comentarios finales de este capítulo

Cuando abrimos los problemas de **Code Forces**, podemos ver que en cada uno de ellos el tamaño de la entrada está especificado, esto le permite a programadores entrenados determinar a priori que tipo de algoritmos usar. Por ejemplo para Shower Line, el problema de fuerza bruta, la entrada máxima es una fila de 5 personas mientras que para el problema de tiempo constante la entrada máxima es de 1.000'000.000.

Por otro lado, cuando hablamos de programa reales los límites son aún más difusos, sin embargo todo lo que hemos aprendido es una guía que bien utilizada, puede ayudarnos a tomar mejores decisiones cuando estemos programando.

> **Pro tip:** se debería practicar los problemas sugeridos, pasar de largo por todos estos conceptos no es suficiente para interiorizalos. Al pricipio pueden parecer difíciles y quizá en ocasiones sea necesario recurrir a las soluciones de otros, pero estudiarlas a conciencia e intentar llegar a respuestas propias, es la mejor forma de mejorar como programadores.

En el siguiente capítulo veremos cómo determinar la complejidad de un algoritmo nada más dando un vistazo al código fuente.

¡Hasta la próxima!
