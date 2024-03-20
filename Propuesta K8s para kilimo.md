
## Deadline

## Contexto

Actualmente la aplicacion de MMRV esta olajada en la nube de Amazon (AWS), pero debido a los compromiso contractuales que tiene el proyecto de MMRV, el proyecto plantea una migracion desde su actual entorno actual en AWS para la nube de de Microsft (Azure).

La aplicacion actualmente usa una solucion contenerizada en AWS, por lo cual una solucion sencilla y segura, seria apuntar para Azure Kubernetes Service(AKS) en la nube de Microsft, que puede administrar y orquestar los contenedores ya existen en AWS sin la necesidad de un cambio mayor o una re-factorizacion de la aplicacion.

## Decision

Kubernetes seria le mejor opción para homologar todo el servicio y no preocuparnos por las herramientas nativas al cambiar de sistemas, puesto kubernetes es un open source que tiene un ecosistema de multiplataformas, permitiendo MMRV alojarse en azure y seguirse comunicando con el resto de aplicaciones alojadas en AWS.

### infraestructura actual
![[Untitled.webp]]
El servicio de MMRV tiene actualmente las imagenes guardas en github y de alli atraves de un pipeline son pusheadas y buildeadas a directamente a los contenedores en AWS
![[CICD-Containers.798e501cfbfc403ac465ff752867ae7d6f3fe4e1.png]]


## diagrama de datos

## detalles **

## Implementacion
LLAMAR A VERONICA
servicio
lado MMRV
digrama

## consecuancias 

 consecuancias de implementar kubernetes  tanto buenas como malas
 - **Desafíos técnicos imprevistos**: por ejemplo, una aplicación puede tener tantas dependencias que la refactorización o el cambio de plataforma pueden ser mucho más complejos y consumir más tiempo de lo que se pensaba en un principio.  
      
    
- **Costos imprevistos**: sin una planificación adecuada, las empresas pueden incurrir en gastos que no habían presupuestado, como nuevas tasas de licencia o costos de capacitación en las nuevas herramientas para los empleados.  
      
    
- **Tiempo de inactividad inesperado**: los cambios importantes en una aplicación pueden generar conflictos o problemas que provoquen un tiempo de inactividad no planificado, tanto en la aplicación como en los sistemas conectados o dependientes.  
      
    
- **Problemas culturales o dificultades en la gestión del cambio**: las distintas organizaciones usan las aplicaciones de manera diferente y esas diferencias pueden generar problemas que ralentizan un proyecto de migración.
## estado


## Propetario 

indique quien es el propietario o responsable de la implementacion 

## Fuente


## Anexo


