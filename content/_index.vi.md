---
title: "Giới thiệu"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

# Public một service và route traffic bằng Subdomain và Path 

![Overview](/fcj-ss2-workshop-002/images/01.webp)

## 1. Overview

Xin chào các bạn trong bài workshop này mình sẽ cùng đồng hành cùng các bạn tìm hiểu 1 khái niệm khá quan trọng trong Kubernetes, đó chính là ingress, và tiến hành public một service và route traffic bằng subdomain và path. 

Đối với K8s thì sẽ có nhiều loại, phiên bản khác nhau, nhưng trong môi trường học tập, làm lab chúng ta có thể dùng các phiên bản nhỏ gọn và nhẹ hơn cả K8s như Minikube, K3s, MicoK8s, ... trong chuỗi series này mình sẽ sử dụng MicroK8s.    

## 2. Objectives

Mục tiêu chuỗi workshop này sẽ giúp các bạn có những khái niệm cơ bản nhất về các khái niệm trong K8s.

Đây cũng sẽ là tiền đề cho nhiều chuỗi workshop sau này về K8s.

## 3. Content

- Giới thiệu về Ingress.
- Cài đặt MicroK8s.
- Cài đặt Ingress Controller.
- Public một service và route traffic bằng subdomain.
- Public một service và route traffic bằng path.

