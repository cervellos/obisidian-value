Docker es una plataforma de creación de contenedores que se usa para desarrollar, distribuir y ejecutar [[Contenedores]]. Docker no usa un hipervisor y se puede ejecutar en equipos de escritorio o en portátiles para desarrollar y probar las aplicaciones. La versión de escritorio de Docker es compatible con Linux, Windows y macOS. En el caso de los sistemas de producción, Docker está disponible para entornos de servidor, incluidos muchas variantes de Linux, Microsoft Windows Server 2016 y versiones posteriores. Muchas nubes, incluida la nube de Azure, son compatibles con Docker.

# ![[Contenedores]]

## Motor docker

![[2-docker-architecture.svg]]

![[Servidor Docker]]
# ![[Imagenes]]
#### Objetos de Docker

Hay varios objetos que creará y configurará para admitir las implementaciones de [[Contenedores]]. Estos incluyen redes, [[Volumenes]] de almacenamiento, complementos y otros objetos de servicio. Aquí no trataremos todos estos objetos, pero es conveniente tener en cuenta que son elementos que se pueden crear e implementar según sea necesario.
## sistema operativo del host 
El sistema operativo del host es el sistema operativo en el que se ejecuta el motor de Docker. Los contenedores de Docker que se ejecutan en Linux comparten el kernel del sistema operativo del host y no requieren un sistema operativo de contenedor, siempre que el archivo binario pueda acceder directamente al kernel del sistema operativo.![[3-container-scratch-host-os.svg]]

## sistema operativo del contenedor
El sistema operativo de contenedor es el sistema operativo que forma parte de la imagen empaquetada. Tenemos flexibilidad para incluir diferentes versiones de los sistemas operativos de Linux o Windows en un contenedor. Esta flexibilidad nos permite tener acceso a determinadas características del sistema operativo o instalar software adicionales que pueden usar nuestras aplicaciones.
![[3-container-ubuntu-host-os.svg]]


## Unionfs
Usamos `Unionfs` para crear imágenes de Docker. `Unionfs` es un sistema de archivos que permite apilar varios directorios, denominados ramas, de tal forma que parece que el contenido está combinado. pero el contenido está separado físicamente. `Unionfs` permite agregar y quitar ramas a medida que se crea el sistema de archivos.
![[3-unionfs-diagram.svg]]

[[Dockerfile]]

## Linux kernel
Docker puede utilizar diferentes interfaces para acceder a las capacidades de virtualizacion del kernel Linux.
![[300px-Docker-linux-interfaces.svg.png]]

![[Dockers/img/5-efficient-use-hardware.svg]]