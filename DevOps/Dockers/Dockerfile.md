Un Dockerfile es un archivo de texto que contiene las instrucciones que se usan para compilar y ejecutar una imagen de Docker. Define los siguientes aspectos de la imagen:

- La imagen base o primaria que usamos para crear la nueva imagen.
- Los comandos para actualizar el sistema operativo base e instalar software adicional.
- Los artefactos de compilación que se incluirán, como una aplicación desarrollada.
- Los servicios que se van a exponer, como la configuración de red y del almacenamiento.
- El comando que se ejecutará cuando se inicie el contenedor.
```
# Step 1: Specify the parent image for the new image
FROM ubuntu:18.04

# Step 2: Update OS packages and install additional software
RUN apt -y update &&  apt install -y wget nginx software-properties-common apt-transport-https \
	&& wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb \
	&& dpkg -i packages-microsoft-prod.deb \
	&& add-apt-repository universe \
	&& apt -y update \
	&& apt install -y dotnet-sdk-3.0

# Step 3: Configure Nginx environment
CMD service nginx start

# Step 4: Configure Nginx environment
COPY ./default /etc/nginx/sites-available/default

# STEP 5: Configure work directory
WORKDIR /app

# STEP 6: Copy website code to container
COPY ./website/. .

# STEP 7: Configure network requirements
EXPOSE 80:8080

# STEP 8: Define the entry point of the process that runs in the container
ENTRYPOINT ["dotnet", "website.dll"]
```

 STEP 8 El `ENTRYPOINT` del archivo indica qué proceso se ejecutará una vez que se ejecute un contenedor a partir de una imagen. Si no hay ningún PUNTO DE ENTRADA u otro proceso para ejecutar, Docker interpretará que no hay nada que hacer en el contenedor y, por tanto, lo cerrará.