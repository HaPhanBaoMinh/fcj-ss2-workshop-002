---
title : "Clear resource"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

Sau khi chúng ta đã tạo ra các resource, các bạn có thể xóa chúng đi khi chúng ta không cần sử dụng nữa. Hoặc vẫn giữ các reource đó cho những Workshop sau.

### Xóa resource

Để xóa resource, chúng ta sử dụng lệnh `kubectl delete` với cú pháp như sau:

    kubeclt delete <resource_type> <resource_name>

Ví dụ, để xóa một Deployment có tên là `nginx-deployment`, chúng ta sử dụng lệnh:

    kubectl delete deployment nginx-deployment

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/25.png)

Kiểm tra xem Deployment đã được xóa chưa:

    kubectl get deployment -A

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/26.png)

Như vậy, không còn thấy Deployment `nginx-deployment` nữa.

