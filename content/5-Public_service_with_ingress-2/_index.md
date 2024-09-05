---
title : "Using Ingress to Route Traffic by Path"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

As mentioned in the previous section, I guided you on how to public a service and route its traffic by subdomain. In this section, I will show you how to use Ingress to route traffic by path.

### 1. Introduction

In simple terms, we will route traffic to a service based on the request's path.

example.com/service1 -> service1

example.com/service2 -> service2

### 2. Create two deployments and services

Here, I create two simple deployments and services using the `nginx` image, using the same two services from the previous section:

![Overview](/images/16.png)

Deploy these two files:

        kubectl apply -f service1.yaml
        kubectl apply -f service2.yaml

Check to make sure everything is fine:

        kubectl get pods

![Overview](/images/17.png)

### 3. Configure Ingress to route traffic

![Overview](/images/18.png)

- **apiVersion: networking.k9s.io/v1**: Declares the API version of Kubernetes that we use for Ingress.
- **kind: Ingress**: The type of resource we are declaring, here it's Ingress.
- **metadata**: Information about the Ingress
  - **name**: The name of the Ingress
  - **annotations**: Additional information for the Ingress
    - **nginx.ingress.kubernetes.io/rewrite-target**: Additional information for NGINX Ingress Controller, used to rewrite the request path to / before sending it to the backend. 
  - **spec**: Configuration information for the Ingress
    - **rules**: The rules that Ingress will use to route traffic to the backend services 
    - **host**: The domain name that Ingress will route traffic to. Here, there are two domains: service1.example.com and service2.example.com.
        - **http**: Configuration for HTTP
          - **paths**: The paths we want to route traffic through
            - **path**: The path that Ingress will route traffic to. In this example, the path is /service1 routing traffic to service1 and /service2 routing traffic to service2.
            - **pathType**: The type of path, here it is Prefix. Prefix means that any request starting with this path will be routed to the backend.
            - **backend:** Backend configuration for the path.
              - **service:** The name of the service that Ingress will route traffic to.
              - **port:** The port of the service that Ingress will route traffic to.
              - **number:** The port number of the service that Ingress will route traffic to. Here, both services are listening on port 80.

Deploy the Ingress configuration file:

      kubectl apply -f ingress.yaml

![Overview](/images/19.png)

Check if the Ingress has been created:

      kubectl get ingress

![Overview](/images/20.png)

We have now created an Ingress to route traffic by path.

### 4. Check the result

First, find the host machine's IP information:

      ifconfig

Here, the host's IP is: 192.168.1.4

To check the result, we need to add a line to the `hosts` file. Currently, I'm using Ubuntu, so the `hosts` file is located at `/etc/hosts`:

      sudo nano /etc/hosts

Add the following line to the `hosts` file:

    192.168.1.4 example.com

![Overview](/images/21.png)

Next, open a browser and access the two URLs `example.com/service1` and `example.com/service2`:

![Overview](/images/22.png)
![Overview](/images/23.png)

We have now successfully used Ingress to route traffic by path.
