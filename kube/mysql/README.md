## mysql

MySQL is an open-source relational database management system (RDBMS) that uses structured query language (SQL). It is developed, distributed, and supported by Oracle Corporation. MySQL is one of the most popular database systems in the world, especially for web applications.

## start minikube

Open your terminal and run the command:

```minikube start```

## create secret

Create mysql secret.

```kubectl create -f mysql-secret.yml -n <namespace>```

To see if the deployment , secret and pod are created successfully.

```kubectl get secret -n <namespace>```

Decode the secret password :

```kubect get secret <secret-name> -n <namespace> -oyaml```

Copy ROOT_PASSWORD value and run.

```echo "<value>" | base64 --decode```

## create deployment

Create mysql deployment.

```kubectl create -f mysql-statefulset.yml -n <namespace>```

To see if the deployment and pod are created successfully.

```kubectl get sts,po,secret -n <namespace>```


## create service

Create mysql service.

```kubectl create -f mysql-service.yml -n <namespace>```

To see if the deployment, service and pod are created successfully.

```kubectl get sts,po,svc,secret -n <namespace>```


## connect to mysql

To connect to the database, we check if the pod is running. Let’s find the name of the pod by executing this commands.

Check the pod name.

```kubectl get sts,po,svc,secret -n <namespace>```

Copy the pod name and run the following command: 

```kubectl exec -it <pod-name> -n <namespace> -- bash```

```mysql -u root -p```

Enter the password ```echo "<value>" | base64 --decode``` and you will be connected to the database. 

If you are connected to the database run:

1- ```show databases;```

2- ```use mysql;```

3- ```show tables;```

4- ```select * from user;```

5- ```select Host,User,Password from user;```

| User | Host      | Password                                  |
|---|---|---|
| root | localhost | *819DF53CFB95644C53BF1CB33671C8BA388DB000 |
| root | %         | *819DF53CFB95644C53BF1CB33671C8BA388DB000 |

Now we have the passwords for localhost and %.

## create database

We need to create a database with the following: 

```create database shop```

### NB
if you want to change the password: 

For MySQL 8.0 and later:

Exemple : ```ALTER USER 'username'@'localhost' IDENTIFIED BY 'new_password';```

For MySQL 5.7 and earlier:

Exemple: ```SET PASSWORD FOR 'username'@'localhost' = PASSWORD('new_password');```

- ```SET PASSWORD FOR 'root'@'localhost' = PASSWORD('new_password'); ```

- ```SET PASSWORD FOR '%'@'localhost' = PASSWORD('new_password'); ```

- ```exit```

- Update the current password on ftm-golang/.env file and on secrets yaml

Now you can connect to your database using the new password. it should work !!!

## Results

|NAME                              |READY   |STATUS    |RESTARTS   |AGE
|---|---|---|---|---|
|pod/mysql-0                       |1/1     |Running   |0          |90m

|NAME                  |TYPE        |CLUSTER-IP      |EXTERNAL-IP   |PORT(S)        |AGE
|---|---|---|---|---|-----|
|service/mysql         |ClusterIP   |10.96.22.219    |<none>        |3306/TCP       |116m

|NAME              |TYPE     |DATA   |AGE
|---|---|---|-----|
|secret/mysecret   |Opaque   |1      |123m

|NAME                     |READY   |AGE
|---|---|----|
|statefulset.apps/mysql   |1/1     |90m