---
title : "ReplicaSet"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 1.4 </b> "
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./05.png)

## 1. ReplicaSet

Để duy trì số lượng Pod ổn định và có khả năng **self-healing** chúng ta có thể sử dụng ReplicaSet. ReplicaSet giúp chúng ta duy trì số lượng pods chạy. 

ReplicaSet sẽ khởi tạo số Pods như chúng ta chỉ định.

Như trên hình vẽ, chúng ta có một ReplicaSet với khởi tạo 2 pod. Nếu vì bất kì lý do gì, 1 trong 2 pod đó có vấn đề và bị terminate, ReplicaSet sẽ tự động khởi tạo thêm 1 pod khác để đảm bảo số lượng