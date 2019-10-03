### Ejecutando ```dockerd```

^^^^^^
<!-- .slide: data-background="images/tux.png" data-background-size="100vh" data-background-opacity="0.2"-->
### Linux

* Lo más recomendable es ejecutar ```dockerd``` como un demonio del sistema
* Distribuciones que utilicen ```systemd``` (RedHat, CentOS, Fedora, Ubuntu 16.04+, Debian Jessie, etc)
  ```bash
  > systemctl enable dockerd
  > systemctl start dockerd
  ```
* Distribuciones que utilicen Unix System V
   ```bash
   > chkconfig docker on
   > service docker start
   ```

^^^^^^
<!-- .slide: data-background="images/windows.png" data-background-size="100vh" data-background-opacity="0.2"-->
### Windows

* Ejecutarlo como servicio de Windows a traves de "Docker Destop For Windows"

^^^^^^
<!-- .slide: data-background="images/osx.png" data-background-size="100vh" data-background-opacity="0.2"-->
### OS X

* Ejecutarlo como servicio del sistema a traves de "Docker Destop For Mac"

^^^^^^

### Ejecutar ```dockerd``` manualmente

```bash
> dockerd [options]
```