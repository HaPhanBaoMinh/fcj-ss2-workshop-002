---
title: "Nodes"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<b> 1.2 </b>"
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./02.webp)

## 1. Nodes

We have just explored the **Master Node**, and now it's time to look at the **Worker Node**. In each **K8s** cluster, there will be multiple **Nodes**, and they are controlled by the **Master Node**. These nodes can be virtual machines, physical machines, etc. The **Worker Node** consists of the following key components:

- **kubelet**: This is a component that runs on each Node. It receives commands from the **control plane** to execute on each Node. Additionally, **kubelet** reports the status of the **containers** to the **control plane**.

- **kube-proxy**: This is a **network proxy** running on each Node, responsible for networking within the Node.

- **container runtime**: This component is responsible for running the containers.
