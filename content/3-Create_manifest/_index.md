---
title : "Create manifest"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./12.png)

Currently, there are two ways for us to manage resources in K8s:

1. Command-line Interface: With this method, we will use **kubectl** to create and manage resources.

2. YAML manifest: This is the more common method. We will configure the desired service information in a .yaml file, which is called a manifest file. In this file, we will configure values such as replicaset, images, version, etc. In this workshop, we will use method number 2 to create our first service.
