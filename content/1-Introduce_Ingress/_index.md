---
title : "Introduction to Ingress"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1. </b> "
---

![Overview](/fcj-ss2-workshop-002/images/01.webp)

## 1. Why do we need Ingress?

In the previous workshop, I introduced you to concepts like Service, Deployment, Pod, Namespace, etc., and in this article, I will introduce you to Ingress.

In the last workshop, we were able to expose services outside the cluster using NodePort. This method works fine but isn't always the best fit. The total number of ports on a node is limited and cannot scale. If many services need to be exposed, managing these ports becomes challenging.

Moreover, NodePort only allows us to expose services outside the cluster through ports and does not support exposing services via domain names.

Ingress was created to solve this issue. Ingress is a resource in Kubernetes that allows traffic routing from outside the cluster to services inside the cluster.

## 2. The concept of Ingress in Kubernetes

Ingress is a resource in Kubernetes that allows traffic routing from outside the cluster to services inside the cluster.

As illustrated in the image above, when we use ingress, there is only one entry point into the cluster, from which traffic can be routed to various services inside the cluster.

To make it clearer, imagine you have multiple services running inside your k8s cluster, each service like a store in a shopping mall. Ingress acts like a receptionist at the entrance of the mall, guiding customers (external requests) to the correct store (service) they need.

## 3. Components of Ingress

Ingress consists of two main components:

- **Ingress Rule**: A resource in Kubernetes that defines how to route traffic from outside to services inside the cluster.

- **Ingress Controller**: A daemon that makes routing decisions based on information from the Ingress Resource.

We will dive deeper into Ingress Rule and Ingress Controller in the following sections.
