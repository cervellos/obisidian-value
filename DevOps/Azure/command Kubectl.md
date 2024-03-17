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
Kubectl edit
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
Kubectl exec
```
: permite ejecutar un comando dentro de un contenedor

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
Kubectl -n [namespace] get pods -o yalm
```
: permiter ver los pod en ese namespace. -o wide para ver la yalm del pod

```
kubectl describe pod [name]
```
: estados del pod y eventos

```
kubectl get all
```
:permite ver los pod y servicios

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








