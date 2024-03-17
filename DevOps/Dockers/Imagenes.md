Una imagen de contenedor es un paquete portátil que contiene software. Cuando se ejecuta esta imagen, se convierte en nuestro  contenedor. los [[Contenedores]] son la instancia en memoria de una imagen.

Las imágenes de contenedor son inmutables. Una vez que haya creado una imagen, no podrá cambiarla. La única forma de cambiar una imagen es crear una nueva. Esta característica es nuestra garantía de que la imagen que usamos en el equipo de producción es la misma que se usa en los equipos de desarrollo y de control de calidad.

#### Cómo compilar una imagen


Usamos el comando `docker build` para compilar imágenes de Docker. Supongamos que usamos la definición de Dockerfile anterior para compilar una imagen. El siguiente ejemplo muestra el comando de compilación de [[Dockerfile]]


``` bash 
docker build -t temp-ubuntu .

```
Esta es la salida que genera el comando de compilación:

Output


```
Sending build context to Docker daemon  4.69MB
Step 1/8 : FROM ubuntu:18.04
 ---> a2a15febcdf3
Step 2/8 : RUN apt -y update && apt install -y wget nginx software-properties-common apt-transport-https && wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && dpkg -i packages-microsoft-prod.deb && add-apt-repository universe && apt -y update && apt install -y dotnet-sdk-3.0
 ---> Using cache
 ---> feb452bac55a
Step 3/8 : CMD service nginx start
 ---> Using cache
 ---> ce3fd40bd13c
Step 4/8 : COPY ./default /etc/nginx/sites-available/default
 ---> 97ff0c042b03
Step 5/8 : WORKDIR /app
 ---> Running in 883f8dc5dcce
Removing intermediate container 883f8dc5dcce
 ---> 6e36758d40b1
Step 6/8 : COPY ./website/. .
 ---> bfe84cc406a4
Step 7/8 : EXPOSE 80:8080
 ---> Running in b611a87425f2
Removing intermediate container b611a87425f2
 ---> 209b54a9567f
Step 8/8 : ENTRYPOINT ["dotnet", "website.dll"]
 ---> Running in ea2efbc6c375
Removing intermediate container ea2efbc6c375
 ---> f982892ea056
Successfully built f982892ea056
Successfully tagged temp-ubuntu:latest

```