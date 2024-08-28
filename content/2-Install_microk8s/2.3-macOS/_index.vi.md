---
title : "macOS"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

### 1. Install MicroK8s on macOS

    brew install ubuntu/microk8s/microk8s

    microk8s install

![Overview](/fcj-ss2-workshop-002/images/1-Basic_concepts./10.png)

### 2. Check the status while Kubernetes starts

    microk8s status --wait-ready


### 3. Turn on the services you want

    microk8s enable dashboard

    microk8s enable dns
    
    microk8s enable registry


### 4. Start using Kubernetes

    microk8s kubectl get all --all-namespaces
