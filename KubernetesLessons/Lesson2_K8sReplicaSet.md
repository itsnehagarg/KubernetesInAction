## Replica Controllers and Replica Sets in K8s

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
It will create 3 replicas as mentioned in the rc definition file above and you can check that using the command:

```
kubectl get replicationcontroller
 ```

![image](https://github.com/itsnehagarg/KubernetesInAction/assets/20385826/ca01c3f1-e040-42d7-ae89-eb5c8c944fad)

All the pods have starting nae as nginx which shows that these pods are created by the replication controller.

# Replica Sets

```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: guestbook
    tier: frontend
spec:
  # modify replicas according to your case
  replicas: 3
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: php-redis
        image: gcr.io/google_samples/gb-frontend:v3

```

## Diff between Replica Sets & RC: Selectors in RS is mandatory but it is not a mandatory one in RC

Replica Sets require a selector definition in its yaml file. It helps in determining what pods will fall under it if we have provided the pods definition file.

Replica Sets can also create pods that we have not created in RS definition yaml file. Selectors provide match labels.

### Commands used with Replica Sets:

```
kubectl create -f replicaset-definition.yml
```

```
kubectl get replicaset
```

```
kubectl get pods
```

### Advantages of Replica Sets:

- Replica SEts can be used to monitor to already existing pods that have already been created.
- If the pods are not created, Replica Sets will create it for you.
- Replica Sets will monitor the pods and if any pod fails it will create a new pod for you.
- Labeling the pods during creation of the pods enables RS to know which pods to monitor.
- Under the slector: matchLabels: tier: we will use the same labels that were used during the creation of the pods.
- Scaling of the pods can be done by specifying in Replica Set definition yaml file.

#### Scaling using Replica Sets
1. Scaling of the pods can be done by specifying in Replica Set definition yaml file.
2. Then run the command

```
kubectl replace -f replicaset-definition.yml
```
3. Another way to do it is usning the below command:
```
kubectl scale --replicas=6 -f replicaset-definition.yml
```

## Commands Review:

1. Create new replica set:
```
kubectl create -f replicaset-definition.yml
```
2. Fetch all the existing replica sets:
```
kubectl get replicaset
```

3. It will delete the replicaset along with the underlying pods:

```
kubectl delete replicaset replicaset-name
```
4. Scale replica set from the command line instead of modifying the replicaset yaml file:

```
kubectl scale --replicas=6 -f replicaset-definition.yml
```
5. Replace replica set:
```
kubectl replace -f replicaset-definition.yml
```

## Hands-On Replica sets:

1. Command to get the number of replica sets:  kubectl get replicaset
2. Number of pods are desired in the replica set?













