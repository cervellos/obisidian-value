es un orquestador de [[Contenedores]] o [[Virtual Machines]]
## Ventajas de Kubernetes

![[CV y PROYECT LOGS/img/2-kubernetes-benefits.svg]]
- Recuperación automática: por ejemplo, para reiniciar contenedores con errores o para reemplazar contenedores
    
- Escalado vertical o disminución del número de contenedores implementados de forma dinámica según la demanda
    
- Actualizaciones graduales automáticas y reversiones de contenedores
    
- Administración del almacenamiento
    
- Administración del tráfico de red
    
- Almacenamiento y administración de información confidencial, como nombres de usuario y contraseñas


## POD

* # ![[pods]]
* [[Service]]
* [[deployment]]\ replimen set


# Cluster
![[what-is-kubernetes_beyond-kubernetes-1.svg]]
| / | K8S | API | \ |
| ---- | ---- | ---- | ---- |
| VM | VM | VM | VM |

## Deploy K8s
![[solutions_kubernetes-on-azure_deployment-strategy_how-rollouts-work.avif]]
1. Crear Deploy YALM de un imagen  
      
    
2. Aplique el archivo YAML al clúster a través de kubectl, la interfaz de la línea de comandos de Kubernetes.  
      
    
3. Kubectl envía la solicitud a kube-apiserver, que autentica y autoriza la solicitud antes de registrar el cambio en una base de datos, etcd.  
      
    
4. El registro de kube-controller-manager supervisa de forma continua la presencia de nuevas solicitudes en el sistema y trabaja para conciliar el estado del sistema con el estado deseado, proceso en el que crea recursos ReplicaSets, implementaciones y pods.  
      
    
5. Después de ejecutar todos los controladores, kube-scheduler detecta que existen pods con el estado "pendiente" porque todavía no se han programado para ejecutarse en un nodo. El programador encuentra nodos adecuados para los pods y, a continuación, se comunica con kubelet en cada nodo para tomar el control e iniciar la implementación.


## Work Flow K8s
![[what-is-kubernetes_solution-architecture-diagram.svg]]

## Ejemplo de flujo de trabajo de DevOps con Kubernetes

1. Repita, prueba y depure rápidamente diferentes partes de una aplicación juntas en el mismo clúster de Kubernetes.  
      
    
2. Fusione código mediante combinación e insértelo en un repositorio de GitHub para lograr integración continua. A continuación, ejecute compilaciones y pruebas automatizadas como parte de la entrega continua.  
      
    
3. Compruebe el origen y la integridad de las imágenes de contenedor. Las imágenes se mantienen en cuarentena hasta que pasan un examen.  
      
    
4. Aprovisione clústeres de Kubernetes con herramientas como Terraform. Gráficos Helm instalados por Terraform definen el estado deseado de los recursos y las configuraciones de las aplicaciones.  
      
    
5. Imponga directivas para gobernar las implementaciones en el clúster de Kubernetes.  
      
    
6. La canalización de versión ejecuta automáticamente una estrategia de implementación predefinida con cada código.  
      
    
7. Agregue auditoría de directivas y corrección automática a la canalización de CI/CD. Por ejemplo, solo la canalización de versión tiene permiso para crear nuevos pods en su entorno de Kubernetes.  
      
    
8. Habilite telemetría de las aplicaciones, supervisión del estado de los contenedores y análisis de registros en tiempo real.  
      
    
9. Solucione los problemas con conclusiones e informe de los planes para el próximo spri

