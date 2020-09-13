---
published: true
title: Crear temas para Bootstrap 4 desde Visual Studio
layout: post
license: ccby
tsocurl: http://thescienceofcode.azurewebsites.net/Articles/Show/5b4575cf407d6f33cc0e9d88
---
![Crear temas para Bootstrap 4 desde Visual Studio]({{ site.baseurl }}/images/bootstrap-4-visual-studio.jpg)

{:.img-footer}
[Photo under Public Domain](https://unsplash.com/photos/hpjSkU2UYSU){:target='_blank'}

Aprenderemos como crear fácilmente temas para Bootstrap 4 desde una aplicación ASP Core 2.1 contruída en Visual Studio.

<!--more-->

Para nuestro caso vamos a usar un nuevo kit que permite integrar fácilmente *Bootstrap 4* con NPM desde Visual Studio con ASP Core para la creación de temas personalizados.

### Pre-requisitos

* [Visual Studio 2017](https://visualstudio.microsoft.com/) instalado y actualizado.

* [Web Essentials](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebExtensionPack2017) instalado.

### Preparando el proyecto

* Crearemos un nuevo proyecto Web en Visual Studio 2017. El *StarterKit* que usaremos está optimizado para aplicaciones **ASP Core 2.1 MVC**, puedes encontrar diferencias en esta guía si utilizas otras versiones de ASP Core. *El Kit no es compatible con ASP Net Framework*.

* Vamos a limpiar algunos archivos innecesarios, asi que podemos remover las siguientes carpetas:

  ![Remove these folders](https://equilaterus.github.io/assets/img/bootstrap4starterkit/RemoveFiles.PNG)

### Descargando Bootstrap4.VisualStudio.StarterKit

* Navegamos hasta https://github.com/equilaterus/Bootstrap4.VisualStudio.StarterKit/ y descargamos el repositorio como ZIP.

  ![Download repo](https://equilaterus.github.io/assets/img/bootstrap4starterkit/Download.PNG)

* Abrimos la carpeta donde se encuentra nuestro proyecto. Podemos hacerlo desde Visual Studio (sólo hay que tener en cuenta hacer clic derecho en el proyecto y NO en la solución).

  ![Open folder](https://equilaterus.github.io/assets/img/bootstrap4starterkit/OpenFolder.PNG)

* Copiamos los archivos que están **dentro del ZIP en la carpeta kit** que previamente descargamos desde el repositorio. Se nos preguntará para sobreescribir algunos archivos, decimos que sí. Al final debería verse más o menos así:

  ![Copy files](https://equilaterus.github.io/assets/img/bootstrap4starterkit/CopyFiles.PNG)

### Pasos finales

* Volvemos a nuestro Visual Studio (es recomendado cerrar y reabrir el proyecto antes de proseguir).

* Restauramos los paquetes NPM que nos descargarán jQuery y Bootstrap 4.

  ![Restore NPM](https://equilaterus.github.io/assets/img/bootstrap4starterkit/RestorePackages.PNG)

* Recompilamos el archivo SCSS que está ubicado en *wwwroot/scss/theme.scss* para generar los archivos CSS (luego de este paso, los archivos se recompilarán automáticamente cada vez que modifiquemos el archivo).

  ![Recompile SCSS](https://equilaterus.github.io/assets/img/bootstrap4starterkit/RecompileScss.PNG)

* Activamos el *Bundle on Build* para que automáticamente se minifiquen los archivos y se obtengan las librerías de terceros dentro de nuestro proyecto.

  ![Activate Bundle on build](https://equilaterus.github.io/assets/img/bootstrap4starterkit/BundleOnBuild.PNG)

* Ahora sólo es cuestión de modificar estos archivos para crear un tema único e increíble.

  ![User files](https://equilaterus.github.io/assets/img/bootstrap4starterkit/UserFiles.PNG)

¡Hasta la próxima!
