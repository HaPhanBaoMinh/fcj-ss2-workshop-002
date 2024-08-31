---
title : "Các thành phần của Ingress"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1.1 </b> "
---

![Overview](/images/02.png)


## 1. Cấu trúc của Ingress Resource

### 1.1 Ingress Rule

Ingress Rule là một resource trong Kubernetes, nó định nghĩa cách route traffic từ bên ngoài vào các service trong cluster.

Mỗi HTTP rule sẽ bao gồm các thông tin sau:

  - Thông tin host (không bắt buộc). Nếu có khai báo host cụ thể, rule sẽ chỉ apply cho host đó. Nếu host không được khai báo, thì rule được áp dụng cho mọi http đến.

  - Danh sách paths (ví dụ /testpath như bên trên), mỗi path sẽ có thông tin pathType và một backend (service) tương ứng với port của nó.

  - Một backend là một bộ gồm service và port. HTTP (HTTPS) request mà thỏa mãn điều kiện về host và path sẽ được chuyển tới backend đã khai báo

### 1.2 Path types

Có 2 loại path:

- **Prefix**: Nếu pathType là Prefix, Ingress sẽ route traffic vào service nếu path của request bắt đầu bằng path của rule. Ví dụ: `/service1` và `/service1/api` sẽ được route vào service1.

- **Exact**: Nếu pathType là Exact, Ingress sẽ route traffic vào service nếu path của request bằng path của rule. Ví dụ: `/service1` sẽ được route vào service1 nhưng `/service1/api` sẽ không được route vào service1.

- **ImplementationSpecific**: Nếu pathType là ImplementationSpecific, Ingress Controller sẽ xác định cách route traffic vào service.

## 2. Ingress Controller

Ingress Controller là một daemon, nó sẽ thực hiện các quyết định định tuyến dựa trên thông tin trong Ingress Rule.

Nói một cách dễ hiểu, Ingress Controller giống như một người điều phối và **Ingress Rule** là một bản hướng dẫn cho người điều phối đó để hướng dẫn traffic vào các service trong cluster.


## 3. Ví dụ về Ingress:

        apiVersion: networking.k8s.io/v1
        kind: Ingress
        metadata:
            name: example-ingress
            namespace: default
        annotations:
            nginx.ingress.kubernetes.io/rewrite-target: /
        spec:
            rules:
            - host: example.com
                http:
                paths:
                - path: /service1
                    pathType: Prefix
                    backend:
                    service:
                        name: service1
                        port:
                        number: 80
                - path: /service2
                    pathType: Prefix
                    backend:
                    service:
                        name: service2
                        port:
                        number: 80

- **apiVersion: apps/v1**: Khai báo phiên bản API của Kubernetes mà chúng ta sử dụng cho Ingress.
- **kind: Ingress**: Loại resource mà chúng ta đang khai báo, ở đây là Ingress.
- **metadata**: Thông tin về Ingress.
  - **name**: Tên của Ingress.
  - **namespace**: Namespace mà Ingress thuộc về.
- **annotations**: Các thông tin bổ sung cho Ingress.
  - **nginx.ingress.kubernetes.io/rewrite-target**: Thông tin bổ sung cho Ingress Controller.
- **spec**: Thông tin cấu hình cho Ingress.
  - **rules**: Các rule của Ingress.
    - **host**: Domain name mà Ingress sẽ route traffic vào.
    - **http**: Cấu hình cho giao thức HTTP.
      - **paths**: Các đường dẫn mà Ingress sẽ route traffic vào.
        - **path**: Đường dẫn mà Ingress sẽ route traffic vào.
        - **pathType**: Loại đường dẫn.
        - **backend**: Cấu hình backend cho đường dẫn.
          - **service**: Tên service mà Ingress sẽ route traffic vào.
          - **port**: Port của service mà Ingress sẽ route traffic vào. 
            - **number**: Port của service mà Ingress sẽ route traffic vào.

Với file cấu hình trên, Ingress sẽ route traffic từ domain `example.com` vào 2 service `service1` và `service2` thông qua đường dẫn `/service1` và `/service2`.
