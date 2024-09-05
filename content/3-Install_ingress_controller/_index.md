---
title : "Installing Ingress Controller"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

In this article, I will use MicroK8s to install the Ingress Controller and use Nginx Ingress Controller as an example.

### 1. Installing Ingress Controller using the Add-on
The ingress feature is available as an Add-on in MicroK8s, making the installation quite simple.

        microk8s enable ingress

After installation, we will see a new Pod created:

![Overview](/fcj-ss2-workshop-002/images/03.png)
![Overview](/fcj-ss2-workshop-002/images/04.png)

However, I will now guide you through installing the Ingress Controller using Helm, in case you are not using MicroK8s or want more customization.

### 2. Installing Ingress Controller using Helm

First, I will disable the Ingress Add-on:

        microk8s disable ingress

![Overview](/fcj-ss2-workshop-002/images/05.png)

Next, we will install Helm:

        sudo snap install helm --classic

![Overview](/fcj-ss2-workshop-002/images/06.png)

After installing Helm, we will add the Nginx Ingress Controller Helm repository:

        helm repo add nginx-stable https://helm.nginx.com/stable
        helm repo update

Next, we will install the Nginx Ingress Controller:

        helm install nginx-ingress ingress-nginx/ingress-nginx
