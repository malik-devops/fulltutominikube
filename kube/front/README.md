## start minikube

Open your terminal and run the command:

```minikube start```

## add secrets

Kubernetes Secrets are secure objects that store sensitive data, such as passwords, OAuth tokens, and SSH keys, with encryption in clusters. To secure your docker credentials, update this command line by adding your username, email and password.

```kubectl -n <namespace> create secret docker-registry registry-secret \ --docker-server=https://index.docker.io/v1/ \ --docker-username=<user-name> \ --docker-password=<user-name> \ --docker-email=<user-email>```

## create deployment

Create a deployment with the new image pushed on dockerhub.

```kubectl create -f ui-deploy.yml -n <namespace>```

To see if the deployment and pod are created successfully.

```kubectl get deploy -n <namespace>```

## add service

Create a service from the react-app deployment.

```kubectl create -f ui-service.yml -n <namespace>```

To see if the deployment and pod are created successfully.

```kubectl get svc -n <namespace>```

To view the project run on your terminal:

```minikube service product-ui --url -n project```

