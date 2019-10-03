### Arquitectura

* Docker Server (Docker Deamon , ```dockerd``` o Docker Engine)
* Docker Client
* Docker Images
* Docker Containers

^^^^^^

### Modelo Cliente - Servidor

[![docker-architecture](/images/docker-architecture.svg)<!-- .element: class="plain" -->](https://docs.docker.com/engine/docker-overview/#docker-architecture)


^^^^^^

### Docker server: ```dockerd```

* Escuha, recibe y procesa las peticiones a la API de Docker 
* Gestiona los objetos de docker (imágenes, contenedores, volúmenes y redes)
* Comunicarse con otros procesos ```dockerd``` para gestionar servicios ([Docker services / swarm](https://docs.docker.com/get-started/part3/))

^^^^^^

### Docker client: ```docker```

* Interfaz principal para conectarse a Docker Server ```dockerd```
* Usa la [API de Docker](https://docs.docker.com/engine/api/latest/) para comunicarse con ```dockerd```
* Recuerda que es ```dockerd``` el que realmente ejecuta la orden, no el cliente ```docker```

^^^^^^

### Modelo Cliente - Servidor

[![docker-architecture](/images/docker-architecture.svg)<!-- .element: class="plain" -->](https://docs.docker.com/engine/docker-overview/#docker-architecture)


^^^^^^

### Docker Registries

* Repositorio o almacen de imágenes
* Docker tiene un repositorio público y gratuito de imágenes públicas que se llama [Docker Hub](https://hub.docker.com/)
* ```dockerd``` utiliza Docker Hub por defecto

notes:

Los comandos ```docker pull``` o ```docker run``` hacen uso del Registry para descargarse las imágenes y,
en el caso del último comando, levantar un contenedor.

^^^^^^

### Tipos de repositorios

* **Cloud-based registries**: Las imágenes son almacenadas en la nube en los servidores del proveedor del servicio. Ej: Docker Hub
* **On-premises registries**: Repositorio de imágenes instalable en nuestra propia infraestructura
* **Public registries**: Cualquier usuario puede descargar las imágenes
* **Private registries**: Sólo los usuarios con el permiso adecuado pueden acceder a las imágenes del repositorio

^^^^^^

### Ejemplos de Docker Registries

* [Docker Trusted Registry (DTR)](https://docs.docker.com/ee/dtr/)
* [Red Hat Quay.io](https://quay.io/)
* [Docker Registry](https://docs.docker.com/registry/)
* [Portus](http://port.us.org/)
* [Amazon](https://aws.amazon.com/es/ecr/), 
[Google](https://cloud.google.com/container-registry/), 
[Azure](https://azure.microsoft.com/en-in/services/container-registry/),
[Alibaba](https://www.alibabacloud.com/product/container-registry)
notes:

DTR: 

* DTR se puede instalar dentro la infraestructura de una organización con objeto de instalar distribuir imágenes
privadas dentro de la organización (o en la nube) de forma segura.
* Por ejemplo: se pueden almacenar aquí las imágenes que consumen los sistema de integración contínua para hacer los despliegues automatizados
* Interfaz web para gestión de imágenes de la organización
* Escaneo de seguridad de las imágenes
* Firmado de imágenes
* Integración con LDAP

Se ofrece con un un add-on para Docker Enterprise de tipo Standard o superior.

Quay.io:

Desarrollado por el equipo de CoreOS, [fue adquirida recientemente por Red Hat](https://www.redhat.com/en/blog/faq-red-hat-acquire-coreos).

Ofrece un registro público y privado de imágenes como Docker Hub y DTR. Instalable en la propia infraestructura de
la organización o en formato Cloud.

Docker Registry:

The Registry is a stateless, highly scalable server side application that stores and lets you distribute Docker images. 

Es open source y se distribuye bajo la licencia Apache.

Levanta el repositorio
```bash
docker run -d -p 5000:5000 --name registry registry:2
```

Descarga la imagen de alpine de Docker Hub
```bash
docker pull alpine
```

Marcamos la imagen con tag que apunta a nuestro repositorio
```bash
docker image tag ubuntu localhost:5000/myfirstimage
```

Subimos la imagen (push)
```
docker push localhost:5000/myfirstimage
```

Recuperamos la imagen de nuestro repositorio
```bash
docker pull localhost:5000/myfirstimage
```

Detenemos el contenedor y lo borramos
```bash
docker container stop registry && docker container rm -v registry
```

Portus:

Otro registry de Docker open source:
* Escaneado de imágenes
* Autenticación con OAuth y OpenID
* Gestión de permisos: teams y bloqueo de usuarios
* Application tokens
* LDAP incluido
* Auditoría: registro de eventos relevantes sobre las imágenes
* API Rest
* **Tiene a SuSE detrás**


^^^^^^

### ¿Y cuál escogemos?

* ¿Es una app pública para uso general o es una app de uso interno?
* ¿Es posible almacenar las imágenes en infraestructura externa?
* ¿Cuán escalable debe ser mi repositorio de imágenes?
* Si mi repositorio es público ¿cómo lo encontrará la gente?
* ¿Puedo trabajar con cualquier proveedor? ¿Es el vendor lock-in in problema?
  ¿Podemos trabajar con software libre?

notes: 

Si se trata de una app pública para consumo general, posiblemente Docker Hub sea el lugar
más adecuado para guardarla. Si se trata de una app de uso interno o de la que no queramos distribuir
el código, un repositorio privado será la única opción.

Si las políticas de seguridad de la organización impiden que las imágenes se puedan almacenar fuera de
nuestra infraestructura, necesitaremos un repositorio _on-premises_ y privado.

Si esperamos tener un gran consumo de imágenes (supongamos empresas de cientos de empleados y proyectos
desarrollándose de forma simultánea) tendremos que tener en cuenta el rendimiento que necesitemos alcanzar
con nuestro repositorio _on-premise_. Si no se disponen de los recursos necesarios para realizar los
ajustes y optimizaciones necesarios de la infraestructura, un repositorio en la nube nos resuelve estos problemas
ya que los servicios gestionados se encargan de ello por nosotros. De nuevo, si es necesario disponer de
repositorios _on-premise_ deberemos tener en cuenta estos costes de infraestructura y mantenimiento.

Si queremos que nuestra imagen se encuentre de forma sencilla, la opción más recomendable es Docker Hub ya que
este es el primer lugar al que la mayoría de la gente acuede a buscar las imágenes.

Por último, _Docker Registry_ o _Portus_ son open-source, lo que nos da una alternativa si no queremos
depender de código propietario, discontinuación de software o lock-in.

Otros factores a tener en cuenta:

* Si trabajas con un proveedor de Cloud, utiliza el repositorio de ese proveedor
* Si el repositorio es _on-premise_ mantenerlo en la misma red en la que se hacen los despliegues
* Si tenemos una gran dispersión geográfica, será buena idea poder disponer de replicas en diferentes
geolocalizaciones o disponer al menos un repositorio con CDN que esté lo suficientemente cerca.

Algunas referencias:
* https://sweetcode.io/docker-hub-quay-beyond-container-registry/
* https://stevelasker.blog/2018/11/14/choosing-a-docker-container-registry/
* https://www.redhat.com/en/resources/quay-container-registry-whitepaper 

^^^^^^

### Modelo Cliente - Servidor

[![docker-architecture](/images/docker-architecture.svg)<!-- .element: class="plain" -->](https://docs.docker.com/engine/docker-overview/#docker-architecture)

^^^^^^

### Docker Images

**Una imagen de docker es un conjunto de instrucciones para crear un contenedor**

Veamos un ejemplo: [nginx](https://github.com/nginxinc/docker-nginx/blob/master/stable/alpine/Dockerfile)

^^^^^^

### Docker Containers

**Un contendor es una instancia de una imagen en ejecución**

![wat](/images/wat.jpg)<!-- .element: class="plain fragment" data-fragment-index="1" -->

^^^^^^

### Docker Containers

Un contendor es una instancia de una imagen en ejecución

**Clase / Objeto: Un objeto es una instancia de una clase** <!-- .element: class="plain fragment" data-fragment-index="1" -->

* La clase sería la imagen <!-- .element: class="plain fragment" data-fragment-index="2" -->
* El objeto sería el contenedor <!-- .element: class="plain fragment" data-fragment-index="3" -->

notes:

Una analogía que a mi me ayudó a entender un poco mejor qué es una imagen y qué es un contenedor
es la relación entre Clase (```class```) y objeto. Y es que un objeto es una instancia de una clase.

En Docker ocurre algo parecido. Tenemos una imagen de nginx (siguiendo con el ejemplo que hemos
visto en diapositivas anteriores) y a partir de esa imagen podemos "instanciar" cinco contenedores de nginx.
Evidentemente, si cinco estos contenedores de nginx están en el mismo servidor, no podrán escuchar todos
en el puerto 80.



