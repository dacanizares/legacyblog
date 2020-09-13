---
published: true
title: Estaba equivocado - cosas que dije como profesor
layout: post
tsocurl: http://thescienceofcode.azurewebsites.net/Articles/Show/594862173e67156b40807c39
---
![Estaba equivocado: cosas que dije como profesor]({{ site.baseurl }}/images/equivocado-profesor.jpg)

{:.img-footer}
[Photo By Brendan Church (CC0)](https://unsplash.com/search/photos/ways){:target='_blank'}

Como profesor siempre defendí mi postura con respecto a la programación, y aunque aún creo firmemente en muchas de las cosas que dije, me parece que es lo correcto reconocer que en los últimos meses he descubierto que en varios puntos estaba equivocado.
<!--more-->

1. **Critiqué el Test Driven Development:** lo veía como repetir el código dos veces con la esperanza de que eso evitara errores (aunque algunas empresas sí que lo hacen mal), quizá no lo comprendía bien o mi pensamiento era aún muy obtuso en este tópico. Hoy estoy seguro que los tests escritos de forma inteligente son la mejor forma de garantizar que nuestros componentes y sistemas funcionan como deberían. Además, al momento de hacer integraciones o realizar cambios, no tienes que estar probando manualmente si la línea de código que modificó una persona del equipo introduce nuevos bugs o altera el comportamiento original.

2. **Defendía a Mongo sobre SQL en la mayoría de situaciones:** los que me conocen de hace rato sabrán que siempre me ha parecido más cool el mundo NoSQL, sin embargo, en los últimos proyectos que hemos realizado, nos hemos encontrado con innumerables problemas a la hora de implementar soluciones con Mongo. Con SQL tenemos varios ORM que hacen gran parte del trabajo por nosotros y si necesitamos hacer una consulta extraña, un par de inner joins suelen solucionar el problema. En cambio, con Mongo tenemos que pegarnos de un driver documentado a medias, pensar mucho mejor las operaciones que tenemos que realizar y con base en ello definir de forma distinta las estructuras, y ni hablar de hacer consultas extrañas.

   Al final, creo que la productividad con Mongo (en nuestro stack dotnet core) es muy inferior comparada con Entity Framework + SQL Server. Así que la próxima vez recomendaría que lo piensen dos veces antes de escoger entre un tipo de DB u otro, quizá al final la diferencia en performance no es tan grande como para justificar el esfuerzo adicional que hay que realizar; peor aún, quizá la solución NoSQL termina por ser más lenta.

3. **Como programadores tendemos a sobrevalorar las tecnologías por su nivel de dificultad:** a todos nos ha pasado que vemos como menos al que programa en una u otra herramienta sólo porque no hace parte del top of the mind. Para explicarme mejor pondré dos ejemplos:

    * Una empresa X estaba desarrollando un software Y (que era relativamente sencillo) con el framework de moda para frontend, luego de varios meses de retraso terminaron por quitarles el proyecto y dárselo a otro equipo que usando el viejo y feo jQuery implementó la solución en mucho menos tiempo. Ahora, no quiero decir que no se actualicen, al contrario hay que conocer tantas tecnologías como sea posible para saber cuando vale realmente la pena usar la nueva y potente superherramienta, o cuando es mejor usar la herramienta en la que ya tu equipo tiene experiencia.

    * Es muy difícil encontrar programadores que tengan un buen nivel para desarrollar vistas usando CSS o algún preprocesador como SASS o LESS; en la teoría este es un trabajo sencillo que los diseñadores deberían realizar, pero en la realidad resulta que construir la parte visual de nuestras aplicaciones es un trabajo arduo al que muy pocos se le miden. Así que la próxima vez que pienses que el CSS y HTML es algo fácil, bueno piénsalo dos veces antes de ir a decir una burrada.

Para terminar, quiero compartir las palabras del programador y exprofesor Ricardo Galli.

> "**No te adelantes, no te dejes seducir por puestos de dirección, gestión o representación.** durante los primeros 20 años de carrera sólo **preocúpate de aprender y practicar** para ser un experto de élite en el área en que estás trabajando. Cuando la domines creerás que lo sabes todo pero en realidad no sabes nada, aprende una nueva y repite el proceso: **ganarás tanta humildad como conocimiento**".
