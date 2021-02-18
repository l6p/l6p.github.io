---
sort: 1
title: Prerequisite
---

# Prerequisite

## Installing Docker Desktop

```warning
Ignore this step if you already have a K8s cluster or don't plan to use it on your own desktop.
```

First make sure you have the desktop version of Docker installed.
If you haven't installed it yet, please open [this page](https://www.docker.com/products/docker-desktop){:target="_blank"} and follow the instructions.

Once installed you can follow [the instructions](https://docs.docker.com/docker-for-mac/#kubernetes){:target="_blank"} to enable Kubernetes on Mac,
or follow [the instructions](https://docs.docker.com/docker-for-windows/#kubernetes){:target="_blank"} to enable Kubernetes on Windows.

Once enabled, you can use the command

```shell
kubectl version --short
``` 

to check the version of the Kubernetes.

## Installing Helm

The Helm tool is required for the installation of Lollipop, and the components it depends on.
If you have not installed Helm, please open [this page](https://helm.sh/docs/intro/install){:target="_blank"} and follow the instructions.

Once installed, you can use the command

```shell
helm version --short
``` 

to check the version of the Helm.

## Creating Namespaces

Creates the K8s namespaces for the system and runtime components of Lollipop:

```shell
kubectl create ns l6p-system 
kubectl create ns l6p-space
```

## Installing MongoDB

Download or clone [this project](https://github.com/l6p/helm){:target="_blank"} and go to the `utils/mongodb` directory.
Please change the **values.yaml** file according to your requirements, and run the command:

```shell
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install mongodb -n l6p-system -f ./values.yaml bitnami/mongodb
```

## Installing Kafka

Lollipop uses Kafka as a message queue to store the logs generated during testing.

Download or clone [this project](https://github.com/l6p/helm){:target="_blank"} and go to the `utils/kafka` directory.
Please change the **values.yaml** file according to your requirements, and run the command:

```shell
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install kafka -n l6p-system -f ./values.yaml bitnami/kafka
```

## Installing K8s Ingress Controller

```warning
Ignore this step if your K8s cluster already has an Ingress controller.
```

Lollipop provides a web-based management platform. In order to use this feature, the Ingress controller must be installed on k8s.

First create a K8s namespace for NGINX Ingress controller:

```shell
kubectl create ns ingress-nginx
```

NGINX Ingress controller can be installed via Helm:

```shell
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx/
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx
```

To check if the ingress controller pods have started, run the following command:

```shell
kubectl get pods -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx --watch
```
