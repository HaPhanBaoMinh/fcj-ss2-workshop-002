---
title : "Ubuntu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

### 1. Install MicroK8s on Linux

    sudo snap install microk8s --classic

    sudo snap alias microk8s.kubectl kubectl


### 2. Check the status while Kubernetes starts

    microk8s status --wait-ready

### 3. Turn on the services you want

    microk8s enable dashboard

    microk8s enable dns
    
    microk8s enable registry

### 4. Start using Kubernetes

    microk8s kubectl get all --all-namespaces
