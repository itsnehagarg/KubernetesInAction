# Kuberenetes Deployments in detail


The deployment.yaml file is similar to services.yaml file. However, we have changed the kind of deployment.yaml file to Deployment. A sample file is shown below:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

## To create a deployment use the below command:
```
kubectl create -f deployment-definition.yaml
```
## To get the deployments:
```
kubectl get deployments
```
#### Deployment automatically creates a new replica set and we see a new replica sets created when we run the command to get the replica sets.
```
kubectl get replicaset
```
#### And replica sets will automatically create pods so when we fetch the list of pods we can view the pods that were created by the replica sets:
```
kubectl get pods
```
![image](https://github.com/itsnehagarg/KubernetesInAction/assets/20385826/fa079347-90e8-4bfd-90d6-0f428c8f79ec)

## To view all the objects that were created using one command, use the below cmd:

```
kubectl get all
```

![image](https://github.com/itsnehagarg/KubernetesInAction/assets/20385826/a2d83ca3-accf-426b-bb8f-1edc492a1e40)


