
# Working with core Kubernetes

## Using Minikube
```
minikube start
```

## Using Docker Desktop - Set kubernetes context
```
 kubectl config use-context docker-desktop
```

## Only when you DO NOT have a local image to work with:
* Sample .NET Core Web App image:
```
docker run -it --rm -p 8000:80 --name aspnetcore_sample mcr.microsoft.com/dotnet/samples:aspnetapp
```

## Retag and push to docker hub:
```
docker login <username>
Username: <username>
Password: <password>
docker images
docker tag <source image> <username>/<target image>:<tag>
docker push <username>/<target image>:<tag>
```


## K8s Management Techniques
* https://kubernetes.io/docs/concepts/overview/working-with-objects/object-management/

## Imperative Deployment

### Deploy the app:
```
kubectl create deployment <your-name>01 --image=<username>/<target image>:<tag> --replicas=2

kubectl get deployments

kubectl describe deployment <your-deployment-name>

kubectl expose deployment < your-deployment-name> --type=LoadBalancer --port=80 --target-port=80 #map service port 80 to container port 80

kubectl scale deployment < your-deployment-name> --replicas=3
```

### Update the app:
Retag and push v2 of the image to docker hub 
```
kubectl set image deployment/<your-deployment-name> <container-name>= <username>/<target>:v2 --record=true
```
Verify the upgrade 
```
Kubectl describe deployment <deployment-name>
```
### Kubernetes rollouts and rollbacks
Get the revision history of your deployment
```
kubectl rollout history deployment/<deployment-name>
```
Rollback your deployment to the previoud version
```
kubectl rollout undo deployment/<deployment-name>
```
Rollback your deployment to a specific version
```
kubectl rollout undo deployment/<deployment-name> --to-revision 1

```


## Spin up Pods and Deployments using declarative method
* Add deployment.yaml -- Generate the YAML file using K8s extention in VS code
* Add service.yaml -- Generate the YAML file using K8s extention in VS code
* Apply the above desired state:
```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
