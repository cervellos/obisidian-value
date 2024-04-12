 ```
kubectl --help
```
: comando de auida

```
Kubectl get [node, ns]
```
: obtener ya sea un nodo o namespace

```
Kubectl create
```
: crea un recurso de un documento

```
Kubectl edit [nombre del archivo]

i modo insertar

:qa #para salir sin save

:wq #salir y aguardar
```
: editar un recurso

```
Kubectl delete elimina un recurso
```
: elimina un recurso

```
Kubectl apply
```
: aplica un manifiesto o configuracion 


```
Kubectl exec [pod name] -it -- bash
```
: permite ejecutar un comando dentro de un contenedor. -it es interactive terminal

```
Kubectl logs
```
: obtiene los logs del contenedor o pod

```
Kubectl cp
```
: copia archivos de la maquina al contenedor

```
Kubectl port-forward
```
: forward un puerto o varios de la maquina hacia el pod

```
Kubectl cordon
```
:  marcar al nodo para que no reciba mas contenedores

```
Kubectl uncordon
```
: desmarca al nodo para que reciba contenedores
```
Kubectl drain
```
: drena el nodo para poder moverlo

```
Kubectl config get contexts
```
: te da el contexto en el archjivo .confg
```
Kubectl -n [namespace] 
```
: permiter correr el comando dentro del namespace

```
Kubectl -n [namespace] get pods
```
: permiter ver los pod en ese namespace

```
Kubectl -n [namespace] get pods -o wide
```
: permiter ver los pod en ese namespace. -o wide expande la informacion

```
Kubectl -n [namespace] get pods [nombre del pod] -o yaml > [nombre del archivo] 

```
: permiter ver los pod en ese namespace. -o yalm para ver la yalm del pod > [nombre del archivo] 

```
kubectl describe pod [name]
```
: estados del pod y eventos

```
kubectl get all
```
:permite ver los pod y servicios

```
k scale deploy  deployment-backend-staging -n backend --replicas=1
```
:permite desacalar replicas de un pod 
## kubectx + kubens
kubectx es plugins para cambiar rapido de cluster en [[kubectl]]
kubens es plugins para cambiar entre namespaces facilmente

```
kubectx [context]
```
: cambia a otro cluster que es en kubeconfig

```
kubectx -
```
: cambia a atras hacia el cluster previo

```
kubectx [context new]=[context old]
```
: renombra contexto

```
kubens kube-system
```
: cambia el namespace activo en kubectl

```
kubens -
```
: va atras en el previo namespace

```
kubectl create secret tls backend-ssl-secret

-n backend --cert=tls.crt --key=tls.key
```

:crea un secreto en tls




