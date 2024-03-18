## start minikube

Open your terminal and run the command:

```minikube start```

## add secrets

Kubernetes Secrets are secure objects that store sensitive data, such as passwords, OAuth tokens, and SSH keys, with encryption in clusters. To secure your docker credentials, update this command line by adding your username, email and password.

```kubectl -n <namespace> create secret docker-registry registry-secret \ --docker-server=https://index.docker.io/v1/ \ --docker-username=<user-name> \ --docker-password=<user-name> \ --docker-email=<user-email>```

## create deployment

Create a deployment with the new image pushed on dockerhub.

```kubectl create -f api-deploy.yml -n <namespace>```

## get pod and deployment

To get pod and deployment, run the following command:

```kubectl get po,deploy,svc -n <namespace>```

You can also log the pod to see informations or warning if the pod is not running. 

```kubectl logs <pod-name> -n <namespace>```


## add service

Create a service from the go-app deployment.

```kubectl create -f api-service.yaml -n <namespace>```

To get service run the following command:

```kubectl get svc -n <namespace>```

To view the project run on your terminal:

```minikube service product-api --url -n project```

