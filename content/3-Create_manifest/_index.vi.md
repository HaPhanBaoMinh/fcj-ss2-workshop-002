---
title : "Create manifest"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

![Overview](/fcj-ss2-workshop-002/images/1-Basic_concepts./12.png)

Hiện tại có 2 cách để chúng ta có thể quản lý các resources trong K8s

1. Command-line Interface: Với cách này, chúng ta sẽ sử dụng **kubectl** để tạo, quản lý các resource. 

2. YAML manifest: Đây là cách thông dụng hơn. Chúng ta sẽ cấu hình các thông tin về service mà chúng ta mong muốn trong 1 file .yaml, đây gọi là file manifest, trong file này sẽ cấu hình các giá trị như replicaset, images, version, ... Trong workshop này chúng ta sẽ dùng cách số 2 để tạo ra servie đầu tiên.

