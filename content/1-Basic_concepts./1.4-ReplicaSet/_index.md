---
title: "ReplicaSet"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: "<b> 1.4 </b>"
---

![Overview](/fcj-ss2-workshop-002/images/1-Basic_concepts./05.png)

## 1. ReplicaSet

To maintain a stable number of Pods and ensure **self-healing** capabilities, we can use a ReplicaSet. ReplicaSet helps us maintain the number of running Pods.

ReplicaSet will initialize the number of Pods as specified.

As shown in the diagram, we have a ReplicaSet that initializes 2 Pods. If for any reason one of those Pods encounters an issue and is terminated, the ReplicaSet will automatically create another Pod to maintain the desired number.
