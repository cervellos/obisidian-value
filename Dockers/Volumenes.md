 ### ¿Qué es un volumen?

Un volumen se almacena en el sistema de archivos del host en una carpeta específica. Elija una carpeta donde sepa que los procesos que no son de Docker no van a modificar los datos.

[[Dockers]] crea y administra el nuevo volumen mediante la ejecución del comando `docker volume create`. Este comando puede estar incluido en la definición de Dockerfile, lo que significa que se pueden crear volúmenes como parte del proceso de creación del contenedor. Docker creará el volumen, si este no existe, la primera vez que intente montarlo en un contenedor.

Hay otra opción disponible para los contenedores de Windows: puede montar una ruta de [[acceso SMB]] como volumen

kubernetes volumn