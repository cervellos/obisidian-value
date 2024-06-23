set de contenedores

Los _Pods_ son las unidades de computación desplegables más pequeñas que se pueden crear y gestionar en Kubernetes.

Un Pod modela un "host lógico" específico de la aplicación: contiene uno o más contenedores de aplicaciones relativamente entrelazados.


# Vida util de pod
![[pod.svg]]
_Un Pod de múltiples contenedores que contiene un extractor de archivos y un servidor web que utiliza un volumen persistente para el almacenamiento compartido entre los contenedores._

## pod networking
cada pod comparte si IP con los contenedores que contenga
