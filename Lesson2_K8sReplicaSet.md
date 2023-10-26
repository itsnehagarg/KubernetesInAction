## Replica Controllers

Why do we need Replication Controller?

- High Availability: RC ensures that the specified number of pods are running all the time. So, if one pof fails it brings up another pod which ensures high availability.
- Load balancing & Scaling:

Replication Controller is an older technology that has been now replaced by Replica set. However, both of them perform the same functions.
Replica Set is a new way to ensure that above requirements are met.

## How to create a Replication Controller?

Create a replication controller yaml file. An example is controllers/replication.yaml :
``` apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx
spec:
  replicas: 3
  selector:
    app: nginx
  template:
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80

```
Once we are ready with the file, we can run the below command:

```
kubectl create -f replication.yaml
```






