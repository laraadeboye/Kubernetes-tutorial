
# BASIC KUBERNETES COMMANDS
Credit to Kodekloud learning platform.


## Notes
To get the number of running pods:

`kubectl get pods`

To create a new pod in kubernetes with an nginx image: (Useful tip: kubectl run command helps to create a yaml file when we specify the -o yaml flag and redirect it to the name of the file using >)

`kubectl run nginx --image=nginx --restart=Never`

To get the images used to create a pod:
To get the number of containers used for a pod:
Check the state of images:

`kubectl describe pod`

To get the nodes the pods are running in:

`kubectl get pods -o wide`
`kubectl describe pod newpods-<id>` (check the node field)

To delete pod

`kubectl delete pod <name of pod>`


## Example
How to create a sample pod named redis and image name redis123 by using a pod-definition YAML file. Note that the image is wrong and will be renamed. This tutorial will demonstrate how to edit the image in the definition file:

- First, use kubectl run command with --dry-run=client -o yaml option to create a manifest file (You can use the --dry-run=client flag to preview the object that would be sent to your cluster, without really submitting it):-

   `kubectl run redis --image=redis123 --dry-run=client -o yaml > redis-definition.yaml`

- Next, use kubectl create -f command to create a resource from the manifest file

   `kubectl create -f redis-definition.yaml`

- Verify the work by running kubectl get command :-
    
    ```kubectl get pods```

- View a summary of the commands below:

   `kubectl run redis --image=redis123   --dry-run=client -o yaml > redis-definition.yaml`
   `kubectl create -f redis-definition.yaml`
   `kubectl get pods`

  ## How to edit the name of the image in the definition file.

- First, use the kubectl edit command to update the image of the pod to redis:

   `kubectl edit pod redis` assuming redis is the name of the pod.

- If you used a pod definition file then update the image from redis123 to redis in the definition file via Vi or Nano editor and then run kubectl apply command to update the image :

   `kubectl apply -f redis-definition.yaml`
- Verify by running:

   `kubectl get pods`


## Replicasets

To get the number of Replicasets or check the readiness of the replicaset:

`kubectl get replicaset`  or 
`kubectl get rs`

To get the image or other details used to create the replicaset:

`kubectl describe rs <name of replicaset>`

To check for the version of replicaset:

```kubectl api-resources | grep replicaset```

To create replicaset:

`kubectl create -f </root/replicaset-definition-1.yaml>` Assuming name of file

To delete replicaset or replicaset file

`kubectl delete replicaset <replicaset-name>` or `kubectl delete -f <file-name>.yaml`

To edit replicaset:

`kubectl edit replicaset <new-replica-set>` Assuming name of replicaset

To scale replicas:

`kubectl scale rs new-replica-set --replicas=6` assuming you want to scale up to 6. 
or use the ```kubectl edit``` command and modify the file.

## Deployment
To get the number of Deployment:

`kubectl get deployment`or 
`kubectl get deploy`

To create deployment: 

`kubectl create -f <deployment-defination.yaml>` assuming name of file.

To get help :
`kubectl create deployment --help`


## sample code block for a deployment.yaml file for httpd:2.4-alpine image

```
---

apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      name: httpd-frontend
  template:
    metadata:
      labels:
        name: httpd-frontend
    spec:
      containers:
      - name: httpd-frontend
        image: httpd:2.4-alpine

  ```


To get the status of the rollout of the deployment:

`kubectl rollout status deployment/<name of deployment>`

To check the history and revisions of rollout:

`kubectl rollout history deployment/<name of deployment>`

To update your deployment use:

`kubectl edit deployment/<name of deployment>` (then update or edit the necessary parameters)

  for editting the image specifically, use:

  `kubectl set image <name of deployment> \ <name of container>=<name of image>`

  for example: 

  `kubectl set image deployment\myapp-deployment \ nginx-container=nginx:1.8.1`

Then apply the update:

`kubectl apply -f deployment-definition.yml`

To undo a change in the rollout:

`kubectl rollout undo deployment <name of deployment>`









