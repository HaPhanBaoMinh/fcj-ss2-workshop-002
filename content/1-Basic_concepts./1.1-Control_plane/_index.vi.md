---
title : "Control Plane"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1.1 </b> "
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./02.webp)

## 1. Control Plane

**Control Plane** hay **Master Node** chịu trách nhiệm điều kiển K8s cluster của chúng ta, trong control place gồm nhiều thành phần. Tuy nhiên trong phạm vi workshop lần này mình sẽ giới thiệu cho các bạn các thành phần chính sau:

- **kube-api-server**: Là thành phần chịu trách nhiệm xử lý tất cả các request đến hệ thống Kubernetes. 

- **etcd**: Đây là một database dạng key value, để chứa thông tin về k8s.

- **kube-scheduler**: Khi chúng ta tạo mới một container thì đây sẽ là thành phần lựa chọn node để chúng ta đặt các container.

- **kube-controller-manager**: Đây là thành phần đảm bảo rằng trạng thái thực tế của các tài nguyên trong cụm Kubernetes luôn khớp với trạng thái mong muốn mà người dùng đã chỉ định. Ví dụ chúng ta tạo ra một replicaset với 3 pod chạy thì **kube-controller-manager** sẽ đảm bảo rằng sẽ luôn có 3 pod được chạy.

- **cloud-controller-manager**: Đối với một số cụm K8s được triển khai trên cloud thì đây là thành phần giúp K8s có thể giao tiếp với các cloud platforms.



