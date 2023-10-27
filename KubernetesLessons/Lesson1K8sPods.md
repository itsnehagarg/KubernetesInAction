# ✨ Some basic commands for Pods in Kubernetes:

### 1. how many pods exists in the system?

kubectl get pods


### 2. kubectl run --help


### 3. create a new pod with the nginx image.

kubectl run nginx --image=nginx


### 3. Which image is used to create a pod?

kubectl describe pod podname

It will show us the details about the pod. So, we can go into Containers-> it has Image : where we can find the image name


### 4. How to know where are thsee pods kept or placed?

kubectl describe pod podname

That can be determined by looking at the Node: value 

Another way is by looking at the below command.

kubectl get pods -o wide

That can be determined by looking at the Node: value 


### 5. create a new pod with the name redis and with the image redis123

Use a pod-definition YAML file.

cat redis.yaml


kubectl create -f redis.yaml

verify that it is created : kubectl get pods


### 6. Changing an image 


kubectl edit redis.yaml

or

vi redis.yaml


Apply the changes using the command:


kubectl apply -f redis.yaml
