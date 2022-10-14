## Azure Login 
```
Az login 
Az account set -s <id>
Az account show
```

## Login to AKS cluster
```
az account set --subscription b214611b-9a79-4e7e-afb0-3d9785737f10
az aks get-credentials --resource-group VMware-RG --name vmwareaks01
```

## Only when you DO NOT have a local image to work with:
* Sample .NET Core Web App image:
```
docker run -it --rm -p 8000:80 --name aspnetcore_sample mcr.microsoft.com/dotnet/samples:aspnetapp
```

## Retag and push to ACR:
```
docker login tshapelabacr01.azurecr.io
Username: tshapeuser
Password: <password>
docker images
docker tag <source image> tshapelabacr01.azurecr.io/<target image>:<tag>
docker push tshapelabacr01.azurecr.io/<target image>:<tag>
```


## K8s Management Techniques
* https://kubernetes.io/docs/concepts/overview/working-with-objects/object-management/

## Imperative Deployment

* Deploy the app:
```
kubectl create deployment <your-name>01 --image=tshapelabacr01.azurecr.io/<your-image-name>:v1 --replicas=2

kubectl get deployments

kubectl describe deployment <your-deployment-name>

kubectl expose deployment < your-deployment-name> --type=LoadBalancer --port=80 --target-port=80 #map service port 80 to container port 80

kubectl scale deployment < your-deployment-name> --replicas=3
```

## AKS Pods and Deployments using declarative method
* Add deployment.yaml -- Generate the YAML file using K8s extention
* Add service.yaml -- Generate the YAML file using K8s extention
* Apply the above desired state:
```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
