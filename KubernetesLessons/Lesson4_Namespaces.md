## Namespaces in K8s

A Kubernetes namespace provides the scope for Pods, Services, and Deployments in the cluster. Users interacting with one namespace do not see the content in another namespace. A K8s namespaces allows you to organize resources within your namespace.

#### Why do we need Namespaces in K8s?
1. Logical grouping of the resources
2. Resource sharing
3. Different teams can have different namespaces to avoid conflicts
4. Blue/ Green Deployment resource sharing
5. Limit resources access when working with many teams

#### To view the existing namespaces use the below command:
```
kubectl get namespaces
```
![image](https://github.com/itsnehagarg/KubernetesInAction/assets/20385826/61b1c231-9148-4ed8-b55e-33ba60a66e83)

- We can see that K8s provides the above namespaces by default.
- kube-system namespace: We should not create anything in this namespace. The components in this namespace are system processes.
- kube-public: publicly accessible data. By running the below command we get the output of the publicly accessible data.
`` kubectl cluster-info
``
- kube-node-lease: It contains information about the heartbeats of the nodes.
- default

## Two ways to create a namespace:

## 1: We can create our namespace using the below command:

```
kubectl create namespace my-namespace
```

![image](https://github.com/itsnehagarg/KubernetesInAction/assets/20385826/c8dbd406-21e1-4148-a937-8e66752ce0b3)

## 2: Create a new namespace using the below yaml file: Let us call it namespace-dev.yaml (better way to create a namespace):

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
##### By default, components are created in default namespace.

## Creating Components in Namespaces:

#### (1st way) In order to create a component in a specific namespace use the below command :

##### set the “namespace” flag when creating the resource:
```
kubectl apply -f configmap.yaml --namespace=my-namepsace

kubectl apply -f pod.yaml --namespace=test

```

#### (2nd way) Inside the configmap.yaml file itself specify the namespace:

##### You can also specify a Namespace in the YAML declaration.

```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  namespace: test
  labels:
    name: mypod
spec:
  containers:
  - name: mypod
    image: nginx

```


References:

https://cloud.google.com/blog/products/containers-kubernetes/kubernetes-best-practices-organizing-with-namespaces






