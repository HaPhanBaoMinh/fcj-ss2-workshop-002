---
title: "Control Plane"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<b> 1.1 </b>"
---

![Overview](/fcj-ss2-workshop-002/images/1-Basic_concepts./02.webp)

## 1. Control Plane

**Control Plane** or **Master Node** is responsible for controlling our K8s cluster. The control plane consists of several components. However, within the scope of this workshop, I will introduce the following key components:

- **kube-api-server**: This component is responsible for handling all requests to the Kubernetes system.

- **etcd**: This is a key-value database used to store information about the K8s cluster.

- **kube-scheduler**: When we create a new container, this component selects the node where the container will be placed.

- **kube-controller-manager**: This component ensures that the actual state of the resources in the Kubernetes cluster matches the desired state specified by the user. For example, if we create a replicaset with 3 running pods, the **kube-controller-manager** will ensure that there are always 3 pods running.

- **cloud-controller-manager**: For some K8s clusters deployed on the cloud, this component helps Kubernetes communicate with cloud platforms.
