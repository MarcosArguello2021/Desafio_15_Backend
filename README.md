# **Desafío: LOGGERS, GZIP y ANÁLISIS DE PERFORMANCE**. Curso CoderHouse Backend Node.Js

## Consignas:

Retomemos nuestro trabajo para implementar compresión por Gzip, registros por logueo, y analizar la performance de nuestro servidor.

Incorporar al proyecto de servidor de trabajo la compresión gzip.

Verificar sobre la ruta /info con y sin compresión, la diferencia de cantidad de bytes devueltos en un caso y otro.

Luego implementar loggueo (con alguna librería vista en clase) que registre lo siguiente:

●Ruta y método de todas las peticiones recibidas por el servidor (info)
●Ruta y método de las peticiones a rutas inexistentes en el servidor (warning)
●Errores lanzados por las apis de mensajes y productos, únicamente (error)

Considerar el siguiente criterio:

●Loggear todos los niveles a consola (info, warning y error)
●Registrar sólo los logs de warning a un archivo llamada warn.log
●Enviar sólo los logs de error a un archivo llamada error.log

Luego, realizar el análisis completo de performance del servidor con el que venimos trabajando.

Vamos a trabajar sobre la ruta '/info', en modo fork, agregando ó extrayendo un console.log de la información colectada antes de devolverla al cliente. Además desactivaremos el child_process de la ruta '/randoms'

Para ambas condiciones (con o sin console.log) en la ruta '/info' OBTENER:

1) El perfilamiento del servidor, realizando el test con --prof de node.js. Analizar los resultados obtenidos luego de procesarlos con --prof-process. Utilizaremos como test de carga Artillery en línea de comandos, emulando 50 conexiones concurrentes con 20 request por cada una. Extraer un reporte con los resultados en archivo de texto. Luego utilizaremos Autocannon en línea de comandos, emulando 100 conexiones concurrentes realizadas en un tiempo de 20 segundos. Extraer un reporte con los resultados (puede ser un print screen de la consola).
2) El perfilamiento del servidor con el modo inspector de node.js --inspect. Revisar el tiempo de los procesos menos performantes sobre el archivo fuente de inspección.
3) El diagrama de flama con 0x, emulando la carga con Autocannon con los mismos parámetros anteriores.

Realizar un informe en formato pdf sobre las pruebas realizadas incluyendo los resultados de todos los test (texto e imágenes).

👉Al final incluir la conclusión obtenida a partir del análisis de los datos.

## Como ejecutar el proyecto:

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
* Para probar/testear los diferentes rutas y funcionalidades, se recomienda utilizar [Postman](https://www.postman.com/downloads/)

## Resolución:

Verificamos sobre la ruta /info con y sin compresión:

![1669203795880](image/README/1669203795880.jpg)

Verificamos con artilerry un test de carga en línea de comandos, emulando 50 conexiones concurrentes con 20 request por cada una, una con un console.log y otra sin:

* artillery quick --count 50 -n 20 [http://localhost:8080/info](http://localhost:8080/info) > result_fork_sinConsoleLog.txt
* artillery quick --count 50 -n 20 [http://localhost:8080/info](http://localhost:8080/info) > result_fork_conConsoleLog.txt

![1669211686742](image/README/1669211686742.png)

Modo profiler sin console.log:

* node --prof server.js 8080 FORK

![1669216218639](image/README/1669216218639.png)

Modo profiler con console.log:

* node --prof server.js 8080 FORK

![1669216356792](image/README/1669216356792.png)


* node --prof-process sinConsoleLog-v8.log > result_fork_prof-sinConsole.txt
* node --prof-process conConsoleLog-v8.log > result_fork_prof-conConsole.txt

![1669216706614](image/README/1669216706614.png)

Utilizaremos Autocannon en línea de comandos, emulando 100 conexiones concurrentes realizadas en un tiempo de 20 segundos:

Sin console.log: 

![1669217906640](image/README/1669217906640.png)

Con console.log:

![1669217793691](image/README/1669217793691.png)

Se aprecia los diagramas de flama:

Sin console.log

![1669226882829](image/README/1669226882829.png)

Con console.log

![1669226833107](image/README/1669226833107.png)

## Conclusión:

Se puedo observar que los logs actúan como un proceso bloqueante en la ejecución de las aplicaciones. Si se hace un mal uso de estos, puede generar retardos o cuellos de botellas en algunos casos, sobre el correcto funcionamiento de la aplicación.
