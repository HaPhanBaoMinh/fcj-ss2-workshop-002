---
title : "Windows"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

### 1. [Download](https://microk8s.io/microk8s-installer.exe) the installer for Windows

### 2. Run the Installer

![Overview](/fcj-ss2-workshop-002/images/1-Basic_concepts./08.png)

### 3. Open a command line

![Overview](/fcj-ss2-workshop-002/images/1-Basic_concepts./09.png)

### 4. Check the status while Kubernetes starts

    microk8s status --wait-ready

### 5. Turn on the services you want

    microk8s enable dashboard

    microk8s enable dns
    
    microk8s enable registry

### 6. Start using Kubernetes

    microk8s kubectl get all --all-namespaces
