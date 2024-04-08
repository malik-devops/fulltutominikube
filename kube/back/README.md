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

## add ingress

Create an ingress from the api service.

```kubectl create -f ingress.yaml -n <namespace>```

To get ingress run the following command:

```kubectl get ing -n <namespace>```

Add the url on your local hosts. Go to your terminal and run:

```sudo nano /etc/hosts```

Add ```192.168.49.2    api.product.test```

## Results

|NAME                          |READY   |UP-TO-DATE   |AVAILABLE   |AGE
|---|---|---|---|---|
|deployment.apps/product-api   |1/1     |1            |1           |18m

|NAME                              |READY   |STATUS    |RESTARTS   |AGE
|---|---|---|---|---|
|pod/mysql-0                       |1/1     |Running   |0          |90m
|pod/product-api-f9f8d95ff-dwpbn   |1/1     |Running   |0          |18m

|NAME                  |TYPE        |CLUSTER-IP      |EXTERNAL-IP   |PORT(S)        |AGE
|---|---|---|---|---|-----|
|service/mysql         |ClusterIP   |10.96.22.219    |<none>        |3306/TCP       |116m
|service/product-api   |NodePort    |10.96.226.60    |<none>        |80:31242/TCP   |11m

|NAME              |TYPE     |DATA   |AGE
|---|---|---|-----|
|secret/mysecret   |Opaque   |1      |123m

|NAME                     |READY   |AGE
|---|---|----|
|statefulset.apps/mysql   |1/1     |90m

|NAME                                   |CLASS   |HOSTS              |ADDRESS   |PORTS   |AGE
|---|---|---|---|---|-----|
|ingress.networking.k8s.io/api-ingress      |nginx   |api.product.test             |80      |2h
