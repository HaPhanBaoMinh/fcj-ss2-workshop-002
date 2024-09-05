---
title : "Ingress Components"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1.1 </b> "
---

![Overview](/fcj-ss2-workshop-002/images/02.png)


## 1. Structure of Ingress Resource

### 1.1 Ingress Rule

An Ingress Rule is a resource in Kubernetes that defines how to route traffic from outside into services inside the cluster.

Each HTTP rule contains the following information:

  - Host information (optional). If a specific host is declared, the rule will only apply to that host. If no host is declared, the rule applies to all incoming HTTP traffic.

  - A list of paths (e.g., /testpath as shown above), where each path contains a `pathType` and a corresponding backend (service) with its port.

  - A backend consists of a service and a port. HTTP (HTTPS) requests that satisfy the conditions for the host and path will be routed to the declared backend.

### 1.2 Path Types

There are 2 types of paths:

- **Prefix**: If `pathType` is `Prefix`, Ingress will route traffic to the service if the request path starts with the rule's path. For example: `/service1` and `/service1/api` will both route to `service1`.

- **Exact**: If `pathType` is `Exact`, Ingress will route traffic to the service only if the request path exactly matches the rule's path. For example: `/service1` will route to `service1` but `/service1/api` will not.

- **ImplementationSpecific**: If `pathType` is `ImplementationSpecific`, the Ingress Controller will decide how to route the traffic to the service.

## 2. Ingress Controller

An Ingress Controller is a daemon that makes routing decisions based on the information in Ingress Rules.

In simpler terms, the Ingress Controller acts like a traffic director, and the **Ingress Rule** is a guide for the director to route traffic into services in the cluster.

Popular Ingress Controllers include: Nginx Ingress Controller, Traefik, HAProxy, etc.

In this article, we will use the Nginx Ingress Controller.

## 3. Example of an Ingress:

        apiVersion: networking.k8s.io/v1
        kind: Ingress
        metadata:
            name: example-ingress
            namespace: default
        annotations:
            nginx.ingress.kubernetes.io/rewrite-target: /
        spec:
            rules:
            - host: example.com
                http:
                paths:
                - path: /service1
                    pathType: Prefix
                    backend:
                    service:
                        name: service1
                        port:
                        number: 80
                - path: /service2
                    pathType: Prefix
                    backend:
                    service:
                        name: service2
                        port:
                        number: 80

- **apiVersion: apps/v1**: Declares the Kubernetes API version being used for Ingress.
- **kind: Ingress**: The resource type being declared, in this case, Ingress.
- **metadata**: Information about the Ingress.
  - **name**: The name of the Ingress.
  - **namespace**: The namespace to which the Ingress belongs.
- **annotations**: Additional information for the Ingress.
  - **nginx.ingress.kubernetes.io/rewrite-target**: Extra information for the Ingress Controller.
- **spec**: Configuration details for the Ingress.
  - **rules**: The rules of the Ingress.
    - **host**: The domain name that the Ingress will route traffic to.
    - **http**: Configuration for the HTTP protocol.
      - **paths**: The paths that the Ingress will route traffic to.
        - **path**: The path that the Ingress will route traffic to.
        - **pathType**: The type of the path.
        - **backend**: The backend configuration for the path.
          - **service**: The name of the service that the Ingress will route traffic to.
          - **port**: The port of the service that the Ingress will route traffic to.
            - **number**: The port of the service that the Ingress will route traffic to.

## 3. Example of an Ingress:

        apiVersion: networking.k8s.io/v1
        kind: Ingress
        metadata:
            name: example-ingress
            namespace: default
        annotations:
            nginx.ingress.kubernetes.io/rewrite-target: /
        spec:
            rules:
            - host: example.com
                http:
                paths:
                - path: /service1
                    pathType: Prefix
                    backend:
                    service:
                        name: service1
                        port:
                        number: 80
                - path: /service2
                    pathType: Prefix
                    backend:
                    service:
                        name: service2
                        port:
                        number: 80

With the above configuration file, the Ingress will route traffic from the domain `example.com` to two services `service1` and `service2` via the paths `/service1` and `/service2`.
