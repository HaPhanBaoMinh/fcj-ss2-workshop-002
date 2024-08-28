---
title: "Service"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: "<b> 1.6 </b>"
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./07.png)

## 1. Service

In Kubernetes, a **Service** is an object that defines how to connect and access Pods. Pods typically have a short lifecycle and can be replaced at any time. Therefore, a **Service** provides a stable access point (usually an IP address or DNS) to communicate with those Pods, regardless of whether the Pods are replaced.

There are four main types of services, and we will explore each type in more detail in another workshop:

- **ClusterIP**: This is the default type if no type is specified for the service. With this type, only services within the Kubernetes cluster can access it.

- **NodePort**: The service will open a port on the host node and use the node's IP to expose the service externally. This method is not recommended, as it can be difficult to manage if your Kubernetes cluster has 100 services and opens 100 ports on the node.

- **LoadBalancer**: Used to expose services externally by utilizing the LoadBalancer of cloud providers.

- **ExternalName**
