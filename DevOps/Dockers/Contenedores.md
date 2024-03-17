Un contenedor es un entorno aislado de forma flexible que nos permite compilar y ejecutar paquetes de software. Estos paquetes de software incluyen el código y todas las dependencias para ejecutar aplicaciones de forma rápida y fiable en cualquier entorno informático. Llamamos a estos paquetes _imágenes de contenedor_.

![[4-docker-container-lifecycle-2.png]]


## Cómo ver los contenedores disponibles

Para mostrar los contenedores en ejecución, use el comando `docker ps`. Para ver todos los contenedores en todos los estados, pase el argumento `-a`.
Este es un ejemplo:

```
docker ps -a
```


Output

```
CONTAINER ID    IMAGE        COMMAND         CREATED       STATUS           PORTS        NAMES
d93d40cc1ce9    tmp-ubuntu:latest  "dotnet website.dll …"  6 seconds ago    Up 5 seconds        8080/tcp      happy_wilbur
33a6cf71f7c1    tmp-ubuntu:latest  "dotnet website.dll …"  2 hours ago     Exited (0) 9 seconds ago            adoring_borg
```

Vamos a revisar tres elementos de la salida anterior:
- El nombre de la imagen que aparece en la columna _IMAGE_; en este ejemplo, _tmp-ubuntu: latest_. Observe cómo está permitido crear más de un contenedor a partir de la misma imagen. Se trata de una característica de administración eficaz que puede usar para habilitar el escalado en las soluciones.
    
- El estado del contenedor que se muestra en la columna _STATUS_. En este ejemplo, hay un contenedor que se está ejecutando y otro que ha terminado. Normalmente, el estado del contenedor es el primer indicador de su estado de mantenimiento.
    
- El nombre del contenedor que se muestra en la columna _NAMES_. Además del identificador de contenedor en la primera columna, los contenedores también reciben un nombre. En este ejemplo, no ha proporcionado explícitamente un nombre para cada contenedor y, como resultado, Docker ha dado al contenedor un nombre aleatorio. Para asignar un nombre explícito a un contenedor mediante la marca `--name`, use el comando `run`.
### Almacenamiento dentro del contendor
- **El almacenamiento en el contenedor es temporal.**
- **El almacenamiento del contenedor está acoplado a la máquina host subyacente.**
- **Las unidades de almacenamiento del contenedor ofrecen un rendimiento menor.**

Los contenedores pueden usar dos opciones para conservar los datos. La primera consiste en hacer uso de _[[volúmenes]]_ y la segunda es mediante _[[montajes de enlace]]_.