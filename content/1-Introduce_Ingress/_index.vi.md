---
title : "Giới thiệu về Ingress"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1. </b> "
---

![Overview](/images/01.webp)

## 1. Vì sao cần Ingress?

Trước đó trong workshop mình đã giới thiệu về Service, Deployment, Pod, Namespace, ... và trong bài này mình sẽ giới thiệu cho các bạn về Ingress.

Trong ws trước chúng ta đã có thể expose service ra bên ngoài cluster thông qua NodePort cách này vẫn hoạt động tốt nhưng không phải lúc nào cũng phù hợp, tổng số port trên một node là có hạn và không thể mở rộng, nếu có nhiều service cần expose ra bên ngoài thì việc quản lý port sẽ trở nên khó khăn.

Hơn nữa NodePort chỉ cho phép expose service ra bên ngoài cluster thông qua port, không thể expose service ra bên ngoài cluster thông qua domain name.

Vì vậy Ingress ra đời để giải quyết vấn đề trên, Ingress là một resource trong Kubernetes cho phép route traffic từ bên ngoài vào các service trong cluster.

## 2. Khái niệm về Ingress trong Kubernetes.

Ingress là một resource trong Kubernetes cho phép route traffic từ bên ngoài vào các service trong cluster.

Như hình minh họa ở trên khi chúng ta dùng ingress thì chỉ có 1 cổng đi vào cluster, từ đó có thể route traffic vào các service trong cluster.

Để dễ hiểu hơn, hãy tưởng tượng bạn có nhiều dịch vụ chạy bên trong cụm k8s của mình, mỗi dịch vụ giống như một cửa hàng trong một trung tâm thương mại. Ingress giống như một quầy lễ tân ở lối vào trung tâm thương mại, nơi sẽ hướng dẫn khách hàng (yêu cầu từ bên ngoài) đến đúng cửa hàng (dịch vụ) mà họ cần.

## 3. Các thành phần của Ingress

Ingress bao gồm 2 thành phần chính:

- **Ingress Rule**: Là một resource trong Kubernetes, nó định nghĩa cách route traffic từ bên ngoài vào các service trong cluster.

- **Ingress Controller**: Là một daemon, nó sẽ thực hiện các quyết định định tuyến dựa trên thông tin trong Ingress Resource.

Chúng ta sẽ tìm hiểu chi tiết hơn về Ingress Rule và Ingress Controller trong các phần tiếp theo.