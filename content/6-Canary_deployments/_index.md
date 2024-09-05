---
title : "Configuring Canary Deployments"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

In this article, I will guide you on how to implement Canary Deployments with Ingress.

### 1. What are Canary Deployments?

Canary Deployments are a method of safely and controllably rolling out new software versions. This approach allows you to deploy a new version of the application and direct only a small portion of the traffic to the new version. This helps you test the new version before rolling it out to all users.

![Overview](/fcj-ss2-workshop-002/images/24.png)

### 2. Configuring Canary Deployments for Ingress

We will reuse the two services from the previous section.

I will take service 1 as the old version and service 2 as the new version.

We have the following Ingress configuration file:

![Overview](/fcj-ss2-workshop-002/images/25.png)

Here, I will route 80% of the traffic to service 1 and 20% to service 2.

Deploy the Ingress configuration file:

        kubectl apply -f ingress.yaml

![Overview](/fcj-ss2-workshop-002/images/26.png)

### 3. Check the Result

First, find the host machine's IP information:

      ifconfig

Here, the host's IP is: 192.168.1.4

To check the result, we need to add a line to the `hosts` file. Currently, I'm using Ubuntu, so the `hosts` file is located at `/etc/hosts`:

      sudo nano /etc/hosts

Add the following line to the `hosts` file:

    192.168.1.4 canary.example.com

Next, open a browser and access the domain `canary.example.com`.

![Overview](/fcj-ss2-workshop-002/images/27.png)
![Overview](/fcj-ss2-workshop-002/images/28.png)

We have successfully configured Canary Deployments with Ingress, directing 80% of traffic to service 1 and 20% to service 2.
