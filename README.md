# Introduction

By using Minikube with React and Go, developers can create local Kubernetes development environments to test and deploy React frontend web applications and Go backend services. This enables a rapid and efficient development cycle, providing a consistent and portable development environment similar to a Kubernetes production environment.

## Minikube

Minikube is an open-source tool that simplifies the local deployment of Kubernetes clusters for development and testing purposes. It's commonly used in conjunction with technologies like React and Go to build modern, scalable applications.

You can start your minikube by running this command if it exists on your local machine: 

```minikube start```

If you don't have minikube installed go to the following link : [Minikube](https://minikube.sigs.k8s.io/docs/start/).

Now you can create a namespace application using the following command:

```kubectl create ns <namespace>```

## React

React is a popular JavaScript library for building interactive and dynamic user interfaces. It's widely used in frontend development to create responsive and high-performance web applications.

## Golang

Go, also known as Golang, is an open-source programming language developed by Google. It's appreciated for its simplicity, performance, and native concurrency, making it a popular choice for backend and microservices development.

## Dockerhub

Docker is an open-source platform that enables developers to create, deploy, and run applications in software containers. Docker containers encapsulate an application and its dependencies into an isolated environment, ensuring portability and consistency across different environments, be it development, testing, or production.

if you don't have docker installed [click on this link](https://docs.docker.com/get-docker/). 

Connect to the DockerHub account and sign up or login with your credentials. Now you can create two repositories named `product-ui` and `product-api`.

## About read me files

In ftm-ui and ftm-api documentations you can build and push images on your dockerhub.

In kube you can create and deploy your applications.

This is a simple project named shop. you can create , list and delete a product. 

let's go!!!
