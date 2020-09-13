---
published: true
title: Analicemos el libro Fundamentos de Programación
layout: post
license: ccbysa
tsocurl: http://thescienceofcode.azurewebsites.net/Articles/Show/5624590a0e6ed3e1bc99aa13
---
![Analicemos el libro Fundamentos de Programación]({{ site.baseurl }}/images/libro-fundamentos-programacion.jpg)

{:.img-footer}
Portada del texto que analizaremos hoy.

Hoy nos convoca la triste tarea de hacer una review del libro: "Fundamentos de Programación: Aprendizaje activo basado en casos". La publicación se presenta así misma como algo revolucionario, "utilizando un enfoque moderno desde el punto de vista pedagógico y moderno desde el punto de vista tecnológico". El problema es que falla en ambas empresas, ¡y vaya que falla!
<!--more-->

> **Advertencia**: La siguiente es una opinión personal de una publicación, amparada en el derecho a la libre expresión. En nuestra profesión lo más profundo que está permitido discutir es sobre un lenguaje de programación; el resto de temas parecen estar censurados entre nosotros. Es hora de acabar con esos tabués. Motivado por el compromiso de honestidad intelectual que tengo con mis estudiantes y con quiénes nos leen, comparto esta review. 

> Con respecto a el uso de una parte de la portada del libro analizado: Copyright Disclaimer Under Section 107 of the Copyright Act 1976, allowance is made for "fair use" for purposes such as criticism, comment, news reporting, teaching, scholarship, and research. Fair use is a use permitted by copyright statute that might otherwise be infringing. Non-profit, educational or personal use tips the balance in favor of fair use.

Empecemos hablando de su enfoque moderno desde lo tecnológico, que está enmarcado en el uso de java, un lenguaje inventando en 1995 (no sobra decir lo inexpresivo que resulta para los tiempos que corren), UML el criticado estándar que fue creado en 1996 , la Programación Orientada a Objetos que fue planteada desde finales de los 50's y el horrible IDE, Eclipse (2001). ¿Esto es moderno? ¡Por favor! realmente estamos hablando de un "enfoque empresarial", simple y llanamente son las herramientas que requiere un sector de la mediocre industria del software del país, pero no son modernas, quizá estén de moda en este lado del mundo, pero repito no son modernas. 

Por otro lado, es hablando de lo pedagógico donde encontramos sus peores falencias. El texto parte de la preconcepción errada que comparten muchos gurús y tiene que ver con el hecho de considerar la Programación Orientada a Objetos como algo totalmente diferente de la Programación Imperativa. El libro se salta el paso de enseñar estructuras más simples, para ahogar al estudiante con los conceptos de clases, objetos, atributos y métodos. Si al estudiante le cuesta entender la abstracción que significa tener una variable en memoria, no me imagino qué entenderán por clases... supongo que no mucho, pero el lema del libro parece ser: aprenda cómo construir ventanas en java para resolver los problemas de un cliente, así no entienda mucho. Y esto mis amigos, termina siendo un gran problema, porque el estudiante no aprende programación imperativa ni orientada a objetos, y con razón, porque la una no es más que una breve extensión de la otra. Enseñar qué es una clase a una persona capaz de escribir código medianamente legible utilizando funciones es muy fácil, pero al revés, seamos realistas, no se entiende nada. 

Lo poco que enseña el libro sobre algoritmos es para sentarse a llorar: los códigos son horribles, no se enseñan buenas técnicas de codificación. Aún no sé si es una maña de sudacas, o una misconception de javero, pero se advierte de usar no múltiples retornos por método a expensas de obtener códigos difíciles de leer, no se explican operadores como el break o el continue, ni cuando ni como utilizar el famoso while true. El tan importante manejo de strings para crear aunque sea pequeños parsers, brilla por su ausencia. 

Pero esto no es lo más triste, apenas llegamos a la parte que resulta más horripilante del texto: todo está en términos de ingeniería de software. No se invita al estudiante a crear, no se hace el intento por explicar como funciona ese "invento" por dentro, como se usan los bits para representar elementos del mundo real dentro de la máquina, como se pueden aplicar conceptos matemáticos en la programación, no se mencionan nociones del costo computacional ni de tantos temas apasionantes que encuentras en las Ciencias de la Computación. Allá, en esas páginas oscuras sólo se habla de clientes, requisitos, contratos y otros términos aburridos. Se enseña a programar como una mera habilidad industrial, y no como lo que realmente es, un arte liberal. En otras palabras: la metodología es perfecta para salir a trabajar en una empresa mediocre. 

En general vamos en contravía, imitando sólo las JavaSchools. No vemos qué están haciendo universidades como Harvard para enseñar programación a los más novatos: abrieron un curso previo a CS101 (Introducción a las Ciencias de la Computación), llamado CS50 donde se explican conceptos de computación con Scratch, manteniendo las cosas simples, pero al mismo tiempo conservando la rigurosidad académica, enseñando temas profundos y apasionantes, invitando al estudiante a crear, y no por el contrario matándole la creatividad y la pasión. 

Sin embargo, es mi temor que muchas universidades tomarán este lamentable camino, y sólo dentro de unos años verán el irreparable daño que hicieron a los estudiantes. No más me imagino, que si hoy les cuesta a nuestros estudiantes aprender materias como estructuras de datos, aún teniendo ciertas bases sobre algoritmos, ¿qué será de los futuros programadores que sólo sabrán programación para dummies? (sería ese un mejor título para el libro xD). El día en que nuestros egresados no sepan nada de programación, entendida en el más amplio de sus significados, o peor aún, que tengamos aún menos egresados que ahora, en ese momento si volveremos a explicar lo mágico que resulta crear universos inexistentes a punta de unos y ceros, ese día nos interesaremos por explicarles las cosas increíbles que ocurren dentro de la máquina cuando pulsas un botón del teclado, lo impresionante que es crear imágenes y sonido con números nada más.... por ahora, ¡volvamos a implementar los requisitos que el cliente está pidiendo! 

> Quizá usted esté de acuerdo conmigo, o quizá piense que la ausencia de un título de doctorado en mi carrera le resta cualquier credibilidad a esta review. En cualquier caso, y como tener ese tipo de cartones no está en mis planes, podrían interesarle estos artículos de personas con mucho más recorrido y preparación en CS. 

> [Sobre la crueldad de verdaderamente enseñar Ciencias de la Computación. Prof. Edsger Dijsktra](https://blog.smaldone.com.ar/2006/07/29/que-es-la-computacion/){:target='_blank'}

> [Los Riesgos de las Universidades Java. Joel Spolsky](https://blog.smaldone.com.ar/2010/06/01/los-riesgos-de-las-universidades-java/){:target='_blank'}
