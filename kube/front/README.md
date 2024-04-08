## start minikube

Open your terminal and run the command:

```minikube start```

## create deployment

Create a deployment with the new image pushed on dockerhub.

```kubectl create -f ui-deploy.yml -n <namespace>```

To see if the deployment and pod are created successfully.

```kubectl get deploy,po -n <namespace>```

You can also log or decribe the pod to see informations or warning if the pod is not running. 

```kubectl describe <pod-name> -n <namespace>```

```kubectl logs <pod-name> -n <namespace>```

## add service

Create a service from the react-app deployment.

```kubectl create -f ui-service.yml -n <namespace>```

To see if the deployment and pod are created successfully.

```kubectl get deploy,po,svc -n <namespace>```

To view the project run on your terminal:

```minikube service product-ui --url -n <namespace>```

## add ingress

Create an ingress from the ui service.

```kubectl create -f ingress.yaml -n <namespace>```

To get ingress run the following command:

```kubectl get ing -n <namespace>```

Add the url on your local hosts. Go to your terminal and run:

```sudo nano /etc/hosts```

Add ```192.168.49.2    ui.product.test```


## Results

|NAME                          |READY   |UP-TO-DATE   |AVAILABLE   |AGE
|---|---|---|---|---|
|deployment.apps/product-ui    |1/1     |1            |1           |103s

|NAME                              |READY   |STATUS    |RESTARTS   |AGE
|---|---|---|---|---|
|pod/product-ui-754dcc8ff4-xfg2t   |1/1     |Running   |0          |103s

|NAME                  |TYPE        |CLUSTER-IP      |EXTERNAL-IP   |PORT(S)        |AGE
|---|---|---|---|---|-----|
|service/product-ui    |NodePort    |10.96.152.123   |<none>        |80:31855/TCP   |20s

|NAME                                   |CLASS   |HOSTS              |ADDRESS   |PORTS   |AGE
|---|---|---|---|---|-----|
|ingress.networking.k8s.io/ui-ingress      |nginx   |ui.product.test             |80      |2h

