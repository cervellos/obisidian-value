*YAML Ain't Markup Language* *o manifiesto*
## Kind: [[Pod]]
crear pod
```
apiversion
kind:pod
metadata:
     name: [name]
spec:
  container:
    -name:
     image:
     env: [variable de entonro]
     resources:
     
```

recources/ recurso
estan compuesto por
request: garantizar que siempre tendra disponible 
limits:  los limites que el pod puede usar

readinessProbe: 

## kind: deployment

template para crear [[pod]]

```

```

## kind: DaemonSet
deploy un pod, una vez en cada nodo, 

## kind: StatefulSet
crea un pod que esta atado a un volumen

```
volumeMounts:   
-mountPath:"[ruta]"
 name: [name]
volumeClainTemplate:
...
StorageClassName:  //drive de kubernetes en cloud
```