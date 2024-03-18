## start minikube

Open your terminal and run the command:

```minikube start```

## create deployment

Create a deployment with the new image pushed on dockerhub.

```kubectl create -f api-deploy.yml -n <namespace>```

## get pod and deployment

To get pod and deployment, run the following command:

```kubectl get po,deploy,svc -n <namespace>```

You can also log or decribe the pod to see informations or warning if the pod is not running. 

```kubectl describe <pod-name> -n <namespace>```

```kubectl logs <pod-name> -n <namespace>```


## add service

Create a service from the go-app deployment.

```kubectl create -f api-service.yaml -n <namespace>```

To get service run the following command:

```kubectl get svc -n <namespace>```

To view the project run on your terminal:

```minikube service product-api --url -n <namespace>```

