### Validando la instalación
👌

^^^^^^
```bash
> docker run --rm hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

notes:

Para validar que la instalación se ha realizado correctamente, lo que vamos a hacer es levantar nuestro primer contenedor:

```bash
> docker run --rm hello-world
```

Este comando hará varias cosas:
* Descargará una imagen de docker
* Levantará un contenedor con esa imagen ejecutando el comando de ese contenedor
* Nos muestra la salida del comando que se ha ejecutado dentro del contenedor
* Apaga el contenedor
* Borra el contenedor (opción `--rm`)

^^^^^^

También podemos verificar las versiones que tenemos instaladas:

```bash
> docker info
```

Más información: [documentación de docker](https://docs.docker.com/engine/reference/commandline/info/)

^^^^^^

* El comando `docker info` admite un parámetro `-f` para generar la salida.

* El parámetro `-f` acepta [templates en go](https://golang.org/pkg/text/template/) 😱
  ```bash
  docker info --format '{{json .}}'
  ```