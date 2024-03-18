## mysql

MySQL is an open-source relational database management system (RDBMS) that uses structured query language (SQL). It is developed, distributed, and supported by Oracle Corporation. MySQL is one of the most popular database systems in the world, especially for web applications.

## start minikube

Open your terminal and run the command:

```minikube start```

## create secret

Create mysql secret.

```kubectl create -f mysql-secret.yml -n <namespace>```

To see if the deployment , secret and pod are created successfully.

```kubectl get deploy,po,secret -n <namespace>```

Decode the secret password :

```kubect get secret <secret-name> -n <namespace> -oyaml```

Copy ROOT_PASSWORD value and run.

```echo "<value>" | base64 --decode```

## create deployment

Create mysql deployment.

```kubectl create -f mysql-statefulset.yml -n <namespace>```

To see if the deployment and pod are created successfully.

```kubectl get deploy,po -n <namespace>```

## create service

Create mysql service.

```kubectl create -f mysql-service.yml -n <namespace>```

To see if the deployment, service and pod are created successfully.

```kubectl get deploy,po,svc -n <namespace>```


## connect to mysql

To connect to the database, we check if the pod is running. Let’s find the name of the pod by executing this commands.

Check the pod name.

```kubectl get deploy,po,secret -n <namespace>```

Copy the pod name and run the following command: 

```kubectl exec -it <pod-name> -n <namespace> -- bash```

```mysql -u root -p```

For the default password you enter ```password``` qnd you will be connected to the database. But this password is not configured on api project. 

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

Now we have to change the passwords for user root.

### NB

For MySQL 8.0 and later:

```ALTER USER 'username'@'localhost' IDENTIFIED BY 'new_password';```

For MySQL 5.7 and earlier:

```SET PASSWORD FOR 'username'@'localhost' = PASSWORD('new_password');```

To see the password defined on the secret, run the following command on your terminal. Copy the ROOT_PASSWORD value and decode for exemple ```echo UGFzc0AxMjM0 | base64 --decode```.

6- ```SET PASSWORD FOR 'root'@'localhost' = PASSWORD('new_password'); ```

7- ```SET PASSWORD FOR '%'@'localhost' = PASSWORD('new_password'); ```

8- ```exit```

Now you can connect to your database using the new password. it should work !!!








