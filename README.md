# Aplicación de NodeJS con MongoDB

Este proyecto consiste en una aplicación de Node.js con MongoDB. Esta aplicación se basa en un [proyecto guiado](https://www.coursera.org/projects/containerize-full-stack-nodejs-application-in-docker) de Coursera. Básicamente es un blog simple que permite a los usuarios ingresar sus nombres y comentarios. Utiliza el marco de aplicación web Express, la base de datos MongoDB y el motor de plantillas EJS.

# Pre-requisitos
- Instalar [Node.js](https://nodejs.org/en/) versión 18.16.0
- Instalar Docker:
 - [Docker](https://docs.docker.com/desktop/install/windows-install/) para Windows, en este caso también se instala la herramienta de docker-compose
 - [Docker](https://docs.docker.com/engine/install/ubuntu/) para Ubuntu
 - [Docker-compose](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04) para Ubuntu

# Instalación

#### Instalación local

Si se quiere instalar y ejecutar la aplicación localmente, sin necesidad de despliegue a través de Jenkins, se debe seguir estos pasos:

1. Clonar el repositorio

````
git clone https://github.com/JulianMolina99/NodeJSApp.git
````

2. Navegar al directorio actual de la aplicación.

````
cd "Install Application"
````

3. Construir y ejecutar el proyecto utilizando Docker Compose.
````
docker-compose up --build
````
4. Navegar a http://localhost:3001

#### Despliegue en Jenkins
Si se desea desplegar la aplicación mediante Jenkins, se debe utilizar los archivos Docker y Docker Compose que se encuentran en la raíz del proyecto. Estos están configurados para trabajar con las variables de entorno y otros aspectos específicos del pipeline en Jenkins.

## Estructura del proyecto
La estructura de carpetas de esta aplicación se explica a continuación:

| Nombre | Descripción |
| ------------------------ | --------------------------------------------------------------------------------------------- |
| **coverage** | Contiene el informe de cobertura de las pruebas del código fuente realizado por Jest. |
| **dist** | Contiene el distribuible (o salida) de la compilación del código fuente con Parcel. |
| **src** | Contiene el código fuente de la aplicación |
| **src/__test__** | Contiene los archivos para realizar pruebas unitarias del código fuente. |
| **src/models** | Los modelos definen esquemas que se utilizarán para almacenar y recuperar datos de la base de datos de la aplicación. |
| **src/views** | Contiene las plantillas de la aplicación que se renderizarán en el cliente, en este caso, la plantilla index.ejs. |
| **src**/index.js | Configura y define las rutas de la aplicación Express. También establece la conexión con MongoDB.|
| **src**/server.js | Punto de entrada de la aplicación. Inicia el servidor y escucha en el puerto especificado. |
| .gitignore | Especifica los archivos y directorios que Git debe ignorar al realizar un commit. |
| Jenkinsfile | Este Jenkinsfile invoca una función de librerías compartidas de Jenkins que realiza el pipeline de CI/CD de la aplicación. |
| docker-compose.yml | Define los servicios, redes y volúmenes de la aplicación para Docker Compose. |
| dockerfile | Define los pasos para construir la imagen Docker de la aplicación. |
| package-lock.json | Mantiene un registro exacto de las dependencias y versiones instaladas por npm en el momento de su creación. |
| package.json | Define las dependencias del proyecto, los scripts de construcción y otros metadatos del proyecto. |
| test-report.xml | Contiene el informe de las pruebas unitarias realizadas en el código fuente.


```
├── coverage
│   ├── clover.xml
│   ├── coverage-final.json
│   ├── lcov.info
│   └── lcov-report
│       ├── base.css
│       ├── block-navigation.js
│       ├── favicon.png
│       ├── index.html
│       ├── prettify.css
│       ├── prettify.js
│       ├── sort-arrow-sprite.png
│       ├── sorter.js
│       └── src
│           ├── index.html
│           ├── index.js.html
│           └── models
│               ├── index.html
│               └── Item.js.html
├── dist
│   ├── index.js
│   └── index.js.map
├── docker-compose.yml
├── dockerfile
├── Install Aplication
│   ├── docker-compose.yml
│   └── dockerfile
├── Jenkinsfile
├── LICENSE
├── package.json
├── package-lock.json
├── README.md
├── src
│   ├── index.js
│   ├── models
│   │   └── Item.js
│   ├── server.js
│   ├── __test__
│   │   ├── index.test.js
│   │   ├── item.test.js
│   │   └── views_index.test.js
│   └── views
│       └── index.ejs
└── test-report.xml
```
### Scripts NPM

Todos los diferentes pasos de construcción están orquestados mediante [scripts de npm](https://docs.npmjs.com/misc/scripts).
Los scripts de npm básicamente nos permiten llamar (y encadenar) comandos de terminal a través de npm.

| Script de Npm | Descripción |
| ------------------------- | ------------------------------------------------------------------------------------------------- |
| `start` | Ejecuta el archivo index.js de la carpeta src con Node.js. Se puede invocar con `npm start` |
| `test` | Ejecuta las pruebas unitarias con Jest, genera un informe de cobertura y procesa los resultados de las pruebas con jest-sonar-reporter. Se puede invocar con `npm test` |
| `build` | Construye la aplicación con Parcel, utilizando el archivo index.js de la carpeta src como entrada. Se puede invocar con `npm run build` |

### Dependencias de desarrollo

Las dependencias de desarrollo son módulos que solo se requieren durante el desarrollo de la aplicación, no cuando la aplicación ya está en producción. Estas son las dependencias de desarrollo del proyecto:

- **browserify-zlib**: Proporciona una implementación zlib para su uso con Browserify.
- **chokidar**: Proporciona una interfaz para observar cambios en archivos y directorios.
- **jest**: Un marco para pruebas unitarias en JavaScript.
- **jest-junit**: Un informe JUnit para Jest, útil para integraciones CI/CD.
- **jest-sonar-reporter**: Genera informes compatibles con SonarQube.
- **parcel-bundler**: Un empaquetador web muy útil para construir proyectos JavaScript modernos.
- **supertest**: Proporciona una abstracción para probar APIs HTTP.

## Compilación

La compilación está configurada para hacerse con [Parcel](https://parceljs.org/), un empaquetador web rápido.

```
"parcel-bundler": "1.3.1"
```

### Compilación usando scripts NPM

La compilación se realiza con el siguiente comando:

```
npm run build
```
Este comando generará una versión de producción de la aplicación en la carpeta dist del proyecto. Este directorio contendrá los archivos estáticos y el código JavaScript transpilado listo para ser desplegado en un servidor de producción.

## Pruebas
Las pruebas están escritas utilizando [Jest](https://jestjs.io/) y [supertest](https://www.npmjs.com/package/supertest).

```
"jest": "29.5.0",
"supertest": "6.3.3"
```

### Ejecucion de tests usando scripts de NPM

Las pruebas unitarias se pueden ejecutar con el siguiente comando:
````
npm run test
````
Los archivos de prueba se encuentran en la carpeta src/\_\_test\_\_.

La ejecución de las pruebas con npm run test también generará un informe de cobertura de las pruebas y procesará los resultados de las pruebas con jest-sonar-reporter, lo que resultará en la creación de un archivo test-report.xml en la raíz del proyecto. Este archivo se puede utilizar para visualizar la cobertura de las pruebas y los resultados en herramientas compatibles como SonarQube.


### Hecho con

- [Node.js](https://nodejs.org/en/) - El entorno de ejecución para el backend de JavaScript.
- [npm](https://www.npmjs.com/) - El manejador de dependencias utilizado para instalar y administrar las bibliotecas y herramientas necesarias.
- [Express](https://expressjs.com/) - El framework de Node.js utilizado para crear la API y manejar las rutas y middleware de la aplicación.
- [Mongoose](https://mongoosejs.com/) - Biblioteca de Node.js utilizada para la gestión de la base de datos MongoDB.
- [EJS](https://ejs.co/) - Motor de plantillas para generar vistas HTML dinámicas a partir de los datos de la aplicación.
- [Body-parser](https://www.npmjs.com/package/body-parser) - Middleware utilizado para analizar las solicitudes entrantes en un formato que se puede utilizar con facilidad.
- [Jest](https://jestjs.io/) - Framework de pruebas para JavaScript, utilizado para realizar pruebas unitarias y de integración en la aplicación.
- [Supertest](https://www.npmjs.com/package/supertest) - Biblioteca utilizada junto con Jest para probar las rutas y endpoints HTTP.
- [Parcel](https://parceljs.org/) - Empaquetador de aplicaciones web rápido y sin configuración, utilizado para compilar y preparar la aplicación para producción.

### Autores

- Julian Steven Molina Campos - JulianMolina99

### Licencia
Este proyecto está bajo la Licencia MIT - revisar el archivo LICENSE.md para mas detalles
