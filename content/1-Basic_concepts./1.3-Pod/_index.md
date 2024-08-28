---
title: "Pod"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<b> 1.3 </b>"
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./04.png)

## 1. Pod

A Pod is the smallest unit in K8s, and Pods act as a wrapper around containers. Each Pod can have one or more containers. The containers within the same Pod share the same network and resources of that Pod.

In the example above, in **Pod-1**, you can see it consists of 3 containers: NodeJS, MongoDB, and Redis, and NodeJS can access both of the other containers.

Meanwhile, in **Pod-2**, there is only one container running .Net. Usually, each Pod will have one container.

When a Pod is terminated or deleted, it cannot replace itself. That's why we often use it in conjunction with other objects like **replicaSet** or **deployment** for **self-healing**.
