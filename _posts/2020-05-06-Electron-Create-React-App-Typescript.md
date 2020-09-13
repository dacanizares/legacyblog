---
published: true
title: Guía definitiva - Electron + CreateReactApp + Typescript
layout: post
license: ccby
tsocurl: https://thescienceofcode.azurewebsites.net/Articles/Show/5eb3627bb7ec7c4964d32c76
---
![Electron + CreateReactApp + Typescript]({{ site.baseurl }}/images/electron-cra-ts.png)

Esta es la guía definitiva (y breve) para comenzar a programar en **Electron** usando **Create React App** y **Typescript**. Con este stack, podremos iniciar ágilmente a construir aplicaciones de escritorio multiplataforma, aprovechando los conocimientos previos que tengamos sobre programación web.

Son únicamente 7 breves pasos. ¡Comencemos!

<!--more-->

## Paso 1: Ejecutar Create React App (CRA)

Para comenzar necesitamos crear una aplicación React usando CRA. Con el parámetro *--template* podemos seleccionar la versión de la plantilla que incluye soporte para **Typescript**.

```
npx create-react-app my-app --template typescript
```

## Paso 2: Descargar dependencias adicionales

A continuación, vamos a descargar una serie de librerías necesarias para convertir nuestra aplicación web en una  de escritorio con **Electron**. Para eso, se deben ejecutar los siguientes comandos:

```
npm install --save-dev @rescripts/cli
npm install --save-dev @rescripts/rescript-env
npm install --save-dev concurrently
npm install --save-dev cross-env
npm install --save-dev electron
npm install --save-dev wait-on
npm install --save-dev electron-builder
npm install --save electron-is-dev
```

## Paso 3: Actualizar la sección scripts del package.json

Después de haber finalizado la instalación, debemos abrir el archivo *package.json* y reemplazar toda la sección de **scripts** con el siguiente contenido:

```json
 "scripts": {
    "start": "rescripts start",
    "build": "rescripts build",
    "test": "rescripts test",
    "electron-dev": "concurrently \"cross-env BROWSER=none npm start\" \"wait-on http://localhost:3000 && electron .\"",
    "postinstall": "electron-builder install-app-deps",
    "preelectron-pack": "npm run build",
    "electron-pack": "electron-builder build -wm"
  }
```
Es importante resaltar que la línea **electron-pack** se puede modificar así:

* *electron-builder build -wml* para generar los builds para windows, mac y linux.
* *electron-builder build -w* para generar los builds para windows.
* *electron-builder build -m* para generar los builds para mac.
* *electron-builder build -l* para generar los builds para  linux.
* O cualquier otra combinación de la letras *wml*.

Es probable que se necesite un sistema operativo diferente al compilar para algunos de los destinos. En general, deberiamos dejar únicamente la letra de nuestro sistema operativo. 

Para más información sobre compilaciones multiplataforma [seguir este enlace](https://www.electron.build/multi-platform-build).

## Paso 4: Añadir configuración adicional al package.json

El siguiente paso, consiste en añadir unas secciones al mismo archivo que estabamos modificando en el paso anterior, el *package.json*. Las secciones a agregar son las siguientes:

```json
"main": "public/electron.js",
"homepage": "./",
"author": {
    "name": "Your name",
    "email": "your.email@domain.com",
    "url": "https://your-website.com"
},
"build": {
    "appId": "com.my-website.my-app",
    "productName": "MyApp",
    "copyright": "Copyright © 2019 ${author}",
    "mac": {
        "category": "public.app-category.utilities"
    },
    "win": {
        "target": ["portable", "nsis"]
    },
    "nsis": {
        "oneClick": false,
        "allowToChangeInstallationDirectory": true
    },
    "files": [
        "build/**/*",
        "node_modules/**/*"
    ],
    "directories": {
        "buildResources": "assets"
    }
}
```

Podemos personalizar los datos de la aplicación y del autor. Si hay alguna duda en este paso, [aquí hay un ejemplo de cómo debería quedar el package.json](https://github.com/dacanizares/Electron-CreateReactApp-TypeScript/blob/steps/package.json) después de todos los cambios; NO debemos reemplazar todo el contenido con el ejemplo, ya que las versiones de nuestros paquetes podrían diferir.

## Paso 5: Añadir .rescriptsrc.js

Este y el paso siguiente, nos permiten modificar la configuración del *webpack* sin necesidad de eyectar nuestra aplicación del CRA usando [Rescripts](https://github.com/harrysolovay/rescripts). Esto lo haremos para poder acceder a algunas funciones cómo la [manipulación de archivos locales](https://nodejs.org/api/fs.html) desde nuestro código.

Para tal fin, debemos crear en la raiz del proyecto un archivo de nombre *.rescriptsrc.js*, con el siguiente contenido:

```js
module.exports = [require.resolve('./.webpack.config.js')]
```

## Paso 6: Añadir .webpack.config.js

Luego, es necesario crear otro archivo en la raiz del proyecto con el nombre *.webpack.config.js* y contenido:

```js
module.exports = config => {
  config.target = 'electron-renderer';
  return config;
}
```

## Paso 7: Añadir el punto de entrada

Finalmente, es necesario crear en la carpeta *public* un archivo llamado *electron.js*, que servirá como punto de entrada. Debe llevar el siguiente contenido:

```js
const electron = require('electron');
const app = electron.app;
const BrowserWindow = electron.BrowserWindow;

const path = require('path');
const isDev = require('electron-is-dev');

let mainWindow;

function createWindow() {
  mainWindow = new BrowserWindow({
    width: 900, 
    height: 680, 
    webPreferences: {
      nodeIntegration: true
    }
  });
  mainWindow.loadURL(isDev ? 'http://localhost:3000' : `file://${path.join(__dirname, '../build/index.html')}`);
  if (isDev) {
    // Open the DevTools.
    //BrowserWindow.addDevToolsExtension('<location to your react chrome extension>');
    mainWindow.webContents.openDevTools();
  }
  mainWindow.on('closed', () => mainWindow = null);
  mainWindow.removeMenu();
}

app.on('ready', createWindow);

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});

app.on('activate', () => {
  if (mainWindow === null) {
    createWindow();
  }
});

```

En este punto ya deberíamos tener una aplicación React que arranca con Electron como si fuera una aplicación de escritorio. Para ejecutar en modo de desarrollo (con hot-reloading incluído), podemos usar el siguiente comando: 

```bash
npm run electron-dev
```

Al hacerlo deberíamos ver en una ventana con un browser emebebido. Por defecto se muestran las herramientas de depuración, pero no hay que preocuparse: en la versión de producción desaparecerán.

![Ejecutando nuestra app React en Electrón]({{ site.baseurl }}/images/electron-cra-ts-run.png)

Para empaquetar una versión de producción podemos usar el comando:

```bash
npm run electron-pack
```

## Instrucciones finales

* Si estamos usando GIT y queremos evitar que los archivos generados al empaquetar la versión de producción suban a nuestro repositorio se debe añadir la siguiente línea al *.gitignore*:

  ```
  /dist
  ```
* Si usamos *React-Router*, el único cambio necesario para que corra normalmente la aplicación sería cambiar el componente **BrowserRouter** por un **HashRouter**.

* Para generar la versión de producción estamos usando [electron-builder](https://www.electron.build/), en las modificaciones que hicimos al package.json añadimos algunas configuraciones básicas, pero en la documentación oficial hay más posibilidades de personalización sobre los instaladores o ejecutables finales que se van a crear.

* Finalmente es bueno resaltar que podemos reutilizar la gran mayoría de nuestros conocimientos, ya que lo único que estamos haciendo es embeber una aplicación web en una ventana de escritorio (a la que podemos extender con funciones propias de una aplicación nativa).


Esta guía está basada en los pasos que propone [este tutorial](https://www.codementor.io/@randyfindley/how-to-build-an-electron-app-using-create-react-app-and-electron-builder-ss1k0sfer), he intentado ser lo más breve posible así como añadir algunas correciones y mejoras adicionales.

En caso de dudas, en este [repositorio](https://github.com/dacanizares/Electron-CreateReactApp-TypeScript/tree/steps) se encuentran recompilados [todos los pasos](https://github.com/dacanizares/Electron-CreateReactApp-TypeScript/commits/steps) aquí explicados.

¡Hasta la próxima!