---
title : "Using Ingress to Route Traffic by Subdomain"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

In this article, I will guide you on how to use Ingress to route traffic by subdomain.

### 1. Introduction

We will create two services, each of which will route traffic through a different subdomain.

service1.example.com -> service1

service2.example.com -> service2

### 2. Create two deployments and services

Here, I create two simple deployments and services using the `nginx` image:

![Overview](/fcj-ss2-workshop-002/images/07.png)

Deploy these two files:

        kubectl apply -f service1.yaml
        kubectl apply -f service2.yaml

![Overview](/fcj-ss2-workshop-002/images/08.png)

Check to make sure everything is fine:

        kubectl get pods

![Overview](/fcj-ss2-workshop-002/images/09.png)

### 3. Configure Ingress to route traffic

![Overview](/fcj-ss2-workshop-002/images/10.png)

- **apiVersion: networking.k9s.io/v1**: Declares the API version of Kubernetes that we use for Ingress.
- **kind: Ingress**: The type of resource we are declaring, here it's Ingress.
- **metadata**: Information about the Ingress
  - **name**: The name of the Ingress
  - **annotations**: Additional information for the Ingress
    - **nginx.ingress.kubernetes.io/rewrite-target**: Additional information for NGINX Ingress Controller, used to rewrite the request path to / before sending it to the backend. 
  - **spec**: Configuration information for the Ingress
    - **rules**: The rules that Ingress will use to route traffic to the backend services 
    - **host**: The subdomain we want to route traffic through. Here, there are two domains: service1.example.com and service2.example.com.
        - **http**: Configuration for HTTP
          - **paths**: The paths we want to route traffic through
            - **path**: The path that Ingress will route traffic to. In this example, the path is / on both domains.
            - **pathType**: The type of path, here it is Prefix. Prefix means that any request starting with this path will be routed to the backend.
            - **backend:** Backend configuration for the path.
              - **service:** The name of the service that Ingress will route traffic to.
              - **port:** The port of the service that Ingress will route traffic to.
              - **number:** The port number of the service that Ingress will route traffic to. Here, both services are listening on port 80.

Deploy the Ingress configuration file:

      kubectl apply -f ingress.yaml

![Overview](/fcj-ss2-workshop-002/images/11.png)

Check if the Ingress has been created:

      kubectl get ingress

![Overview](/fcj-ss2-workshop-002/images/12.png)

We have now created an Ingress to route traffic by subdomain.

### 4. Check the result

First, find the host machine's IP information:

      ifconfig

Here, the host's IP is: 192.168.1.4

To check the result, we need to add two lines to the `hosts` file. Currently, I'm using Ubuntu, so the `hosts` file is located at `/etc/hosts`:

      sudo nano /etc/hosts

Add the following two lines to the `hosts` file:

    192.168.1.4 service1.example.com
    192.168.1.4 service2.example.com

![Overview](/fcj-ss2-workshop-002/images/13.png)

Next, open a browser and access the two domains `service1.example.com` and `service2.example.com`:

![Overview](/fcj-ss2-workshop-002/images/14.png)
![Overview](/fcj-ss2-workshop-002/images/15.png)

We have now successfully used Ingress to route traffic by subdomain.
