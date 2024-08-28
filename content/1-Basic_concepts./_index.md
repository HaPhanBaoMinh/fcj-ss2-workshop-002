---
title: "Core Concepts"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<b> 1. </b>"
---

![Overview](/fcj-ss2-workshop-002/images/1-Basic_concepts./03.png)

## 1. What is K8s and why should we use it?

When you search for this question on the internet, you can find many definitions and explanations mentioned. Here is my explanation of this technology.

Imagine that in a construction project, there are many departments responsible for different tasks, such as:

- Construction department
- Logistics department
- Painting department
- Electrical department
- Plumbing department

And the person who coordinates and ensures that these tasks operate smoothly and on schedule is the **contractor**.

In case the construction department is behind schedule, the **contractor** must find a way to add resources to this department by hiring more workers to ensure that the work proceeds as planned without interruption.

In this case, **K8s** can be seen as the **contractor** in the above scenario. **K8s** acts as a coordinator in the system, where each service in the system is like a department in that construction project. When a service encounters a problem (resource shortage, app crash, etc.), **K8s** will play the role of providing additional "workers" by scaling up the **Pods** to handle the workload.

Additionally, there are many other benefits from using **K8s** for deployment. You can refer to more details in this [video](https://www.youtube.com/watch?v=a2gfpZE8vXY).

## 2. Core Concepts in K8s

- Control Plane
- Nodes
- Pod
- ReplicaSet
- Deployment
- Namespace
- Services
- Types of Services

## 3. References

- [Overview - kubernetes](https://kubernetes.io/docs/concepts/overview/)
- [Getting Started with K8s: Core Concepts](https://edgehog.blog/getting-started-with-k8s-core-concepts-135fb570462e)
