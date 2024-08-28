---
title : "Nodes"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 1.2 </b> "
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./02.webp)

## 1. Nodes

Vừa rồi chúng ta đã tìm hiểu **Master Node** bây giờ sẽ đến lượt **Worker Node**, trong mỗi cụm **K8s** sẽ có nhiều các **Node**, và chúng được điều khiển bởi **Master Node**. Các node này có thể là máy ảo, máy vật lý, ... Đối với các **Worker Node** sẽ gồm những thành phần chính sau:

- **kubelet**: Đây là một thành phần chạy trên mỗi Node, nó sẽ nhận lệnh từ **control plane** để thực thi trên mỗi Node, ngoài ra **kubelet** còn báo cáo các trạng thái của các **container** cho **control plane**.

- **kube-proxy**: Đây là một **network proxy** chạy trên mỗi Node, chịu trách nhiệm về phần netword trong Node.

- **container runtime**: Là thành phần chịu trách nhiệm chạy các container.
