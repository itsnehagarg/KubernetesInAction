## Namespaces in K8s

Create a new namespace using the below yaml file: Let us call it namespace-dev.yaml:
```
apiVersion: v1
kind: Namespace
metadata:
  name: development
  labels:
    name: development

```
### Create the development namespace using kubectl by using the below command:
```
kubectl create -f namespace-dev.yaml
```

### We can view the pods in different namespaces using the below mentioned commands:

```
kubectl get pods --namepsace=dev
```
#### For default namespace:
```
kubectl get pods
```
#### For prod namespace:
```
kubectl get pods --namespace=prod
```
