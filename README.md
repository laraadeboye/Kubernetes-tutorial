
# BASIC KUBERNETES COMMANDS
Credit to Kodekloud learning platform.


## Notes
To get the number of running pods:

```kubectl get pods```

To create a new pod in kubernetes with an nginx image:

```kubectl run nginx --image=nginx --restart=Never```

To get the images used to create a pod:
To get the number of containers used for a pod:
Check the state of images:

```kubectl describe pod```

To get the nodes the pods are running in:

```kubectl get pods -o wide```
```kubectl describe pod newpods-<id>``` (check the node field)

To delete pod
```kubectl delete pod <name of pod>```


## Example
How to create a sample pod named redis and image name redis123 by using a pod-definition YAML file. Note that the image is wrong and will be renamed. This tutorial will demonstrate how to edit the image in the definition file:

- First, use kubectl run command with --dry-run=client -o yaml option to create a manifest file (You can use the --dry-run=client flag to preview the object that would be sent to your cluster, without really submitting it):-

   ```kubectl run redis --image=redis123 --dry-run=client -o yaml > redis-definition.yaml```

- Next, use kubectl create -f command to create a resource from the manifest file

   ```kubectl create -f redis-definition.yaml``` 

- Verify the work by running kubectl get command :-
    
    ```kubectl get pods```

- View a summary of the commands below:

   ```kubectl run redis --image=redis123   --dry-run=client -o yaml > redis-definition.yaml```
   ```kubectl create -f redis-definition.yaml```
   ```kubectl get pods```

  ## How to edit the name of the image in the definition file.

- First, use the kubectl edit command to update the image of the pod to redis:

   ```kubectl edit pod redis```

- If you used a pod definition file then update the image from redis123 to redis in the definition file via Vi or Nano editor and then run kubectl apply command to update the image :

   ```kubectl apply -f redis-definition.yaml```
- Verify by running:

   ```kubectl get pods```






