# **Desafío: DESPLEGAR NUESTRO PROYECTO EN LA NUBE**. Curso CoderHouse Backend Node.Js

## Consignas:

Crear un proyecto en Heroku.com para subir el servidor que venimos realizando, reformando todo lo necesario para su correcto funcionamiento en la nube.

Subir el código a Heroku.com, sin olvidar incluir el archivo .gitignore para evitar subir los node_modules. Comprobar que el proyecto inicie de manera correcta en la nube. Verificar que en su ruta raíz se encuentre la página pública del servidor. El servidor debe seguir funcionando en forma local.

Realizar un cambio a elección en alguna vista, probar en forma local y subir nuevamente el proyecto a Heroku, verificando que la nueva reforma esté disponible online.

Revisar a través de una consola local, los mensajes enviados por nuestro servidor en Heroku a su propia consola.

## Como ejecutar el proyecto de manera local:

* Ejecutar el comando `npm install`
* Se debe crear un archivo de configuraracion `.env` con los siguientes datos

```
MONGO_USER = "<usuario Mongo Atlas>"
MONGO_PASS = "<contraseña Mongo Atlas>"
MONGO_CLUSTER = "<@clusterx.asd123.mongodb.net/test>"
GOOGLE_APLICATION_CREDENTIALS = "<google credentials>"
PUERTO = 8080
```

* Ejecutar el comando `npm run start` o ` npm run start -- --puerto <n° de puerto>`
* Para probar/testear los diferentes rutas y funcionalidades, se recomienda utilizar [Postman](https://www.postman.com/downloads/)´

## Como ejecutar el proyecto en la nube:

Ingresar al siguiente enlace:

[Heroku-App](https://coder-backend-heroku.herokuapp.com)
