## Namespaces in K8s

A Kubernetes namespace provides the scope for Pods, Services, and Deployments in the cluster. Users interacting with one namespace do not see the content in another namespace.

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
#### To view the existing namespaces use the below command:
```
kubectl get namespaces
```
![image](https://github.com/itsnehagarg/KubernetesInAction/assets/20385826/61b1c231-9148-4ed8-b55e-33ba60a66e83)

