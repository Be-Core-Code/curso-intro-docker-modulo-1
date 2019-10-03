### Docker Flavours
🍦

^^^^^^

### 🍦Docker flavours 🍦

![Docker flavours](images/docker-flavours.png)<!-- .element: class="plain" -->

Fuente: [Documentación de Docker](https://docs.docker.com/install/overview/)

notes:

## Nightly builds
Nightly builds are created once per day from the master branch. The version number for nightly builds take the format:

0.0.0-YYYYmmddHHMMSS-abcdefabcdef
where the time is the commit time in UTC and the final suffix is the prefix of the commit hash, for example 0.0.0-20180720214833-f61e0f7.

These builds allow for testing from the latest code on the master branch. No qualifications or guarantees are made for the nightly builds.

The release channel for these builds is called nightly.

## Pre-releases
In preparation for a new year-month release, a branch is created from the master branch with format YY.mm when the milestones desired by Docker for the release have achieved feature-complete. Pre-releases such as betas and release candidates are conducted from their respective release branches. Patch releases and the corresponding pre-releases are performed from within the corresponding release branch.

While pre-releases are done to assist in the stabilization process, no guarantees are provided.

Binaries built for pre-releases are available in the test channel for the targeted year-month release using the naming format test-YY.mm, for example test-18.09.

## General availability
Year-month releases are made from a release branch diverged from the master branch. The branch is created with format <year>.<month>, for example 18.09. The year-month name indicates the earliest possible calendar month to expect the release to be generally available. All further patch releases are performed from that branch. For example, once v18.09.0 is released, all subsequent patch releases are built from the 18.09 branch.

Binaries built from this releases are available in the stable channel stable-YY.mm, for example stable-18.09, as well as the corresponding test channel.

Relationship between Docker Engine - Community and Docker Engine - Enterprise code
For a given year-month release, Docker releases both Docker Engine - Community and Docker Engine - Enterprise variants concurrently. Docker Engine - Enterprise is a superset of the code delivered in Docker Engine - Community. Docker maintains publicly visible repositories for the Docker Engine - Community code as well as private repositories for the Docker Engine - Enterprise code. Automation (a bot) is used to keep the branches between Docker Engine - Community and Docker Engine - Enterprise in sync so as features and fixes are merged on the various branches in the Docker Engine - Community repositories (upstream), the corresponding Docker Engine - Enterprise repositories and branches are kept in sync (downstream). While Docker and its partners make every effort to minimize merge conflicts between Docker Engine - Community and Docker Engine - Enterprise, occasionally they will happen, and Docker will work hard to resolve them in a timely fashion.

## Next release
The activity for upcoming year-month releases is tracked in the milestones of the repository.

^^^^^^

### Docker Engine - CE
* Es la que vamos a instalar para el curso
* Tiene tres canales:
  * Stable
  * Test
  * Nightly
* Se mantiene en repositorios públicos

^^^^^^
### Docker Engine - CE

* Versionado: ```YY.mm.<patch>```
  * ```YY.mm``` corresponden al año y mes de la versión a partir de la versión ```18.09```
  * **No sigue [versionado semántico](https://semver.org/)**
  * La cadencia de versiones es aproximadamente de 6 meses
  * ```patch``` puede incluir información adicional como beta, RC, etc.

^^^^^^

### Docker Enterprise

* private image management
* integrated image signing policies
* cluster management with support for Kubernetes and Swarm orchestrators. 
* It allows you to implement node-based RBAC policies, image promotion policies, image mirroring
* scan your images for vulnerabilities. 
* has support with defined SLAs and extended maintenance cycles for patches for up to 24 months.

^^^^^^

### Docker Enterprise

* Se mantiene en repositorios privados de código

[Más información](https://docs.docker.com/ee/supported-platforms/)

