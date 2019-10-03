### 💾 Instalación de Docker: Linux 💾
<!-- .slide: data-background="images/tux.png" data-background-size="100vh" data-background-opacity="0.2"-->

^^^^^^

### Linux
<!-- .slide: data-background="images/tux.png" data-background-size="100vh" data-background-opacity="0.2"-->

* La forma recomendada es utilizar el gestor de paquetes de cada distribución
  * [Centos](https://docs.docker.com/install/linux/docker-ce/centos/)
  * [Debian](https://docs.docker.com/install/linux/docker-ce/debian/)
  * [Fedora](https://docs.docker.com/install/linux/docker-ce/fedora/)
  * [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

^^^^^^

### Métodos alternativos:
<!-- .slide: data-background="images/tux.png" data-background-size="100vh" data-background-opacity="0.2"-->

* [Instalación a partir de binarios](https://docs.docker.com/install/linux/docker-ce/binaries/)
* Descarga e instalación de paquetes ```.rpm``` / ```.deb```

^^^^^^

### 💾 Instalación de Docker: Mac 💾
<!-- .slide: data-background="images/osx.png" data-background-size="100vh" data-background-opacity="0.2"-->

* Descargar [Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)
* Instalar el paquete

notes:

Como se indica en el enlace, para poder instalar Docker en Mac, se necesita:
* Hardware: de 2010 o posterior (debes tener soporte para MMU Virtualization, incluyendo Extended Page Tables (EPT) y Unrestricted Mode). Lo puedes comprobar fácilmente ejecutando ```sysctl kern.hv_support```
* Software: OSX 10.12 o posterior. Docker sólo da soporte a la versión actual de OSX (10.14 en el momento de redactar estas diapositivas) y dos versiones anteriores.
* Al menos 4GB de RAM
* **No tener una versión anterior a VirtualBox 4.3.30 instalada** ya que las versiones anteriores no son compatibles con Docker Desktop.

Podéis encontrar información más detallada en el enlace de la diapositiva.

^^^^^^

### 💾 Instalación de Docker: Windows 💾
<!-- .slide: data-background="images/windows.png" data-background-size="100vh" data-background-opacity="0.2"-->

^^^^^^

### Requisitos del sistema
<!-- .slide: data-background="images/windows.png" data-background-size="100vh" data-background-opacity="0.2"-->

* Windows 10 64-bit: Pro, Enterprise, or Education (Build 15063 o posterior).
* Activar las características Hyper-V y Containers Windows
* Procesador de 64 bit con Second Level Address Translation (SLAT)
* 4GB  RAM
* Activar a nivel de BIOS el soporte de virtualización de hardware
* [Más información sobre virtualización](https://docs.docker.com/docker-for-windows/troubleshoot/#virtualization-must-be-enabled)

^^^^^^

### Instalación
<!-- .slide: data-background="images/windows.png" data-background-size="100vh" data-background-opacity="0.2"-->


* Descargar e instalar "Docker Desktop for Windows"
* Instala los siguientes programaas
  * Docker Engine
  * Docker CLI
  * [Docker Compose](https://docs.docker.com/compose/)
  * [Docker Machine](https://docs.docker.com/machine/overview/)
  * [Kitematic (legacy)](https://docs.docker.com/kitematic/userguide/)

^^^^^^

### Instalación
<!-- .slide: data-background="images/windows.png" data-background-size="100vh" data-background-opacity="0.2"-->

* Una vez instalado dispondremos del icono en la barra del escritorio

![windows systray](images/whale-icon-systray-windows.png)<!-- .element: class="plain"-->


^^^^^^

### Instalación Windows Server
<!-- .slide: data-background="images/windows.png" data-background-size="100vh" data-background-opacity="0.2"-->
```PowerShell
Install-Module -Name DockerMsftProvider -Repository PSGallery -Force
Install-Package -Name docker -ProviderName DockerMsftProvider
Restart-Computer -Force
```

notes:
Revisar la 
[documentación oficial](https://docs.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment) 
de microsoft para la instalación de docker en Windows Server

^^^^^^

### Process Isolation Mode
<!-- .slide: data-background="images/windows.png" data-background-size="100vh" data-background-opacity="0.2"-->

* Modo de ejecución disponible a partir de Docker 18.09.1 y Windows 10 
* En versiones anteriores sólo era posible con Windows Server
* En este modo se pueden usar herramientas como Task Manager o Process Monitor para monitorizar los contenedores
* Restricción en este modo: la versión del kernel de imagen del contenedor debe coincidir con el kernel del host


notes: 

* Información extraída del [siguiente artículo](https://stefanscherer.github.io/how-to-run-lightweight-windows-containers-on-windows-10/)

* Artículo al respecto en el [Blog de Microsoft](https://blogs.msdn.microsoft.com/freddyk/2019/01/13/process-isolation-for-containers-in-windows-10/)

^^^^^^

### Hyper-V Isolation Mode
<!-- .slide: data-background="images/windows.png" data-background-size="100vh" data-background-opacity="0.2"-->

* Los procesos del contenedor se ejecutan sobre un "hypervisor" mínimo que se levanta antes de crear el contenedor
* Esto permite:
  * Ejecutar distintos kernels de windows
  * Levantar contenedores Linux dentro de Windows (LCOW)
* Precio a pagar por tener que levantar un "hypervisor"
  * se tarda más en levantar el contenedor
  * se consumen más recursos

^^^^^^

### LCOW (Linux Containers On Windows)

* Disponible a partir de Windows 10 Professional, Windows 10 Enterprise o Windows Server 2019 **version 1809**
* Permite ejecutar contenedores windows y linux simultáneamente
* Antes de LCOW, Docker Desktop for Windows sólo permite ejecutar contenedores o de windows ode linux, **pero no se podían tener contenedores de de ambos sistemas corriendo a la vez**
* LCOW utiliza *Hyper-V Isolation mode*
* Esta funcionalidad está, a día de hoy en modo experimental

notes:

Antes del desarrollo de la tecnología LCOW, los contenedores en windows tenían una limitación importante:
o ejecutabas contenedores en windows o los ejecutabas en Linux. Esta situación era bastante limitante ya que
si querías desarrollar, por ejemplo, una app en ASP .NET que consumía una API desarrollada en node, 
no podías levantar los contenedores de manera simultánea.

Para poder usar LCOW, según se indica en la [propia documentación del proyecto](https://github.com/linuxkit/lcow), necesitamos:
* Windows 10 Pro or Windows Server 2016 1709 o superior
* Activar las caraterísticas Hyper-V y Container de Windows
* Docker for Windows versión 18.02 o posterior
* Levantar ```dockerd``` en modo experimental (dentro de Docker Desktop ir a _Settings -> Daemon_ y activar 'experimental features')

Una vez hecho esto, podemos levantar un contenedor de linux usando el argumento --platform=linux:

```PowerShell
docker run --platform linux --rm -ti busybox sh
```

Para profundizar sobre este tema, podéis utilizar los siguientes enlaces:
* [repositorio LCOW en github](https://github.com/linuxkit/lcow)
* Documentación oficial sobre LCOW de Microsoft, [aquí](https://docs.microsoft.com/en-us/virtualization/windowscontainers/deploy-containers/linux-containers) y [aquí](https://docs.microsoft.com/en-us/virtualization/windowscontainers/quick-start/quick-start-windows-10-linux)
* [Post oficial en el blog de Docker](https://www.docker.com/blog/docker-for-windows-18-02-with-windows-10-fall-creators-update/)


