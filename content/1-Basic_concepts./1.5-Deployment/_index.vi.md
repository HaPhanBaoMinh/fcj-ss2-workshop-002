---
title : "Deployment"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 1.5 </b> "
---

![Overview](/fcj-ss2-workshop-002/images/1-Basic_concepts./06.png)

## 1. Deployment

Khi một service hay application được triển khai chúng sẽ được update các phiên bản mới một cách liên tục. Khi update các version mới cho các container chúng ta cần một cơ chế update tự động thay vì việc phải update thủ công từng service, việc này sẽ đặc biệt khó khăn khi service của chúng ta có hàng chục thậm chí hàng trăm container. Deployment object sẽ giúp chúng ta xử lý các vấn đề trên. 

Ngoài ra deployment còn các cơ chế rollback nếu version mới gặp sự cố và có khả năng quản lý các phiên bản của deployment, chúng ta có thể rollback về một version cụ thể mà chúng ta mong muốn



