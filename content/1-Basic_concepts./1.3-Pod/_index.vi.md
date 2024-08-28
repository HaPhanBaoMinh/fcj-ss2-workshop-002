---
title : "Pod"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 1.3 </b> "
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./04.png)

## 1. Pod

Pod là thành phần nhỏ nhất trong K8s, các Pod như một lớp bọc cho các container. Mỗi Pod sẽ có thể có 1 hoặc nhiều container. Các container trong cùng 1 Pod sẽ chia sẽ chung 1 mạng và tài nguyên của pod đó.

Trong ví dụ trên ở **Pod-1** ta có thể thấy gồm 3 container, NodeJS, MongoDB, Redis và NodeJS có thể truy cập cả 2 container kia.

Trong khi đó ở **Pod-2** thì chỉ có một container .Net chạy. Thông thường thì mỗi Pod sẽ có một container.

Khi một Pod bị terminated hoặc bị xóa, nó sẽ không thể tự thay thế chính nó. đó là lý do tại sao chúng ta thường dùng nó chung với các object khác như **replicaSet** hay **deployment** để **self-healing**


