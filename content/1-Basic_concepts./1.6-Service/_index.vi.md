---
title : "Service"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 1.6 </b> "
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./07.png)

## 1. Service

Trong Kubernetes, **Service** là một đối tượng giúp định nghĩa cách thức kết nối và truy cập tới các Pod. Các Pod thường có vòng đời ngắn ngủi và có thể bị thay thế bất cứ lúc nào. Vì vậy, một **Service** sẽ cung cấp một điểm truy cập ổn định (thường là một địa chỉ IP hoặc DNS) để giao tiếp với các Pod đó, bất kể các Pod bị thay thế hay không.

Có 4 kiểu service chính, chúng ta sẽ tìm hiểu từng kiểu kỹ hơn vào một workshop khác

- ClusterIP: Đây là kiểu mặc định nếu không chỉ định kiểu cho service, đối với kiểu này thì chỉ các service bên trong cụm k8s mwois có thể access tới được.

- NodePort: Service sẽ mở một port trên node host service đó và sử dụng IP của node đó để expose service ra bên ngoài, cách này không được khuyến khích, hãy tưởng tượng nếu cụm k8s của bạn có 100 service và mở 100 port trên node, sẽ dẫn tới rất khó có thể kiểm soát được.

- LoadBalancer: Được sử dụng để expose các service ra bên ngoài bằng cách sử dụngLoadBalancer của các cloud.

- ExternalName

