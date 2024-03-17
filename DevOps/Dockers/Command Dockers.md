```
docker images  
```
: Enumera las imagenes en el registro

```
docker ps -a 
```
: Para mostrar los contenedores en ejecución, use el comando `docker ps`. Para ver todos los contenedores en todos los estados, pase el argumento `-a`.

```
docker rmi temp-ubuntu:version-1.0
```
:remueve una imagen del resgistro

```
docker build -t temp-ubuntu .
```
:Compila una imagen

```
docker run -d tmp-ubuntu
```
:Use el comando `docker run` para iniciar un contenedor. Solo es necesario especificar la imagen que se va a ejecutar mediante su nombre o identificador para iniciar el contenedor a partir de la imagen. Un contenedor iniciado de esta manera proporciona una experiencia interactiva.

En este caso, para ejecutar el contenedor con nuestro sitio web en segundo plano, agregue la marca `-d`.

```
docker pause happy_wilbur
```
:para pausar el contenedor

```
docker unpause happy_wilbur
```
:anula la suspensión de todos los procesos de los contenedores especificados.

```
docker restart happy_wilbur
```
: Reincia un contenedor

```
docker stop happy_wilbur
```
:El comando "stop" envía una señal de finalización al contenedor y a los procesos que se ejecuta en él.

```
docker rm happy_wilbur
```
: remueve un contenedor especificado

```
 docker volume create
```
: Docker crea y administra el nuevo volumen mediante la ejecución del comando

```
`docker stats`. 
```
: Este comando devuelve información para el contenedor como el porcentaje de uso de CPU, el porcentaje de uso de la memoria, las entradas o salidas escritas en el disco, los datos de red enviados y recibidos, y los id.