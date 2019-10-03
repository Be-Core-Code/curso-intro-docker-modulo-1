# Diapositivas del Curso de Introducción a Docker
## Módulo 1: Instalación de Docker

## Índice

* Versiones de Docker
* Instalación de Docker
* Arquitectura
* Ejecutando ```dockerd```
* Validando la instalación de docker

Para ver las diapositivas:

```bash
> docker run --rm -ti -p "8001:8001" becorecode/curso-intro-docker-modulo-1:latest
```

Una vez levantado el contenedor, accede con un navegador web a `http://localhost:8001`

## Navegación

Las diapositivas están desarrolladas usando [reveal.js](https://revealjs.com/#/):

* Accede a las notas del presentador usando la letra `s`
* Accede a una visión global de todas las diapositivas del módulo usando la tecla `ESC`
* Navega por las diapositivas usando las flechas ⬆➡⬇⬅
* Para imprimirlas:
  * Accede a la URL `http://localhost:8001/?print-pdf`
  * Imprime la página 
  * Si deseas añadir las notas del presentador utiliza la URL  `http://localhost:8001/?print-pdf&showNotes=true`

## Desarrollo

Si quieres contribuir a este repositorio, puedes hacerlo de dos maneras: utilizando docker o sin utilizar docker.

### Contribuir usando Docker

Como se indica un poco más abajo, haz un fork del repositorio y clonalo en tu máquina. 
Asegurate de tener [docker instalado](https://docs.docker.com/install/).

Una vez tengas tu fork clonado, accede a la carpeta con el repsotorio

```bash
> cd /ruta/al/repositorio
```

Estas diapositivas se han desarrollado en una máquina con OSX. Para mejorar el rendimiendo hemos utilizado
volúmenes para cachear los módulos de node. Por ello, antes de poder levantar el contenedor debemos
insertar los módulos de node en volumen. Para ello, ejecutamos el siguiente comando:

```bash
> docker-compose run node npm install grunt-contrib-clean grunt-contrib-nodeunit && node install
```

Finalmente, levantamos el contenedor:
```bash
> docker-compose up
```

Puedes acceder a las diapositivas en `localhost:8001`. Haz los cambios que necesites en las diapositovas situadas en la carpeta
`slides/` y recarga el navegador para ver el resultado.

Si quieres cambiar el puerto, puedes detener los servicios con `docker-compose down`, editar el fichero 
`docker-compose.ymla`, cambiar la configuración del servicio `node` y volver a levantar de nuevo los 
servicios con `docker-compose up`

### Contribuir sin utilizar docker.

**El desarrollo de estas diapositivas se ha hecho usando Docker, por lo que el siguiente procedimiento no ha sido testado
de manera extensiva**

Instala la versión 10 de node. Si sueles trabajar con node y tienes varios proyectos, te recomiendo que 
utilices una herramienta como [nvm](https://github.com/nvm-sh/nvm) para instalar esta versión.

Una vez instalado node y npm instalamos los paquetes de node requiere el proyecto para ejecutarse:

```bash
npm install grunt-contrib-clean && \
    npm install grunt-contrib-nodeunit && \
    npm install
```

Por último, levantamos el servidor:

```bash
npm start
```

Puedes acceder a las diapositivas en `localhost:8000`. Haz los cambios que necesites en las diapositovas situadas en la carpeta
`slides/` y recarga el navegador para ver el resultado.


### ¿Cómo enviar las modificaciones para que se incoporen al repositorio?

* Haz un fork del proyecto
* Cloan el proyecto en tu máquina
* Siguiendo alguno de los procedimientos anteriores, modifica las diapositivas
* Crear una rama en git y haz push de esa rama a tu fork
* Envíanos un pull-request desde github
