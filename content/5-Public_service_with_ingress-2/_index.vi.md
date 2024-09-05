---
title : "Sử dụng Ingress để Route Traffic bằng Subdomain"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

Như phần trước mình đã hướng dẫn các bạn public một service và route traffic của nó bằng subdomain. Trong phần này mình sẽ hướng dẫn các bạn cách sử dụng Ingress để route traffic bằng path.

### 1. Giới thiệu

Có thể hiểu đơn giản là chúng ta sẽ route traffic vào service dựa trên đường dẫn của request.

example.com/service1 -> service1

example.com/service2 -> service2

### 2. Tạo 2 deployment và service

Ở đây mình tạo 2 deployment và service đơn giản và sử dụng image `nginx`, ở đây mình dùng luôn 2 service ở phần trước:

![Overview](/fcj-ss2-workshop-002/images/16.png)

Tiến hành deploy 2 file này:

        kubectl apply -f service1.yaml
        kubectl apply -f service2.yaml

Kiểm tra xem mọi thứ đã ổn chưa:

        kubectl get pods

![Overview](/fcj-ss2-workshop-002/images/17.png)

### 3. Tiến hành cấu hình Ingress để route traffic

![Overview](/fcj-ss2-workshop-002/images/18.png)

- **apiVersion: networking.k9s.io/v1**: Khai báo phiên bản API của Kubernetes mà chúng ta sử dụng cho Ingress.
- **kind: Ingress**: Loại resource mà chúng ta đang khai báo, ở đây là Ingress.
- **metadata**: Thông tin về Ingress
  - **name**: Tên của Ingress
  - **annotations**: Các thông tin bổ sung cho Ingress
    - **nginx.ingress.kubernetes.io/rewrite-target**: Thông tin bổ sung cho NGINX Ingress Controller, dùng để rewrite đường dẫn của request thành / trước khi gửi đến backend. 
  - **spec**: Thông tin cấu hình cho Ingress
    - **rules**: Các quy tắc (rules) mà Ingress sẽ sử dụng để route traffic vào các dịch vụ (service) backend 
    - **host**: Subdomain mà chúng ta muốn route trafficDomain name mà Ingress sẽ route traffic vào. Ở đây, có hai domain: service1.example.com và service3.example.com.
        - **http**: Cấu hình cho HTTP
          - **paths**: Các path mà chúng ta muốn route traffic
            - **path**: Đường dẫn mà chúng ta muốn route traffic Đường dẫn mà Ingress sẽ route traffic vào. Trong ví dụ này, đường dẫn là /service1 route traffic vào service1 và /service2 route traffic vào service2.
            - **pathType**: Loại path, ở đây là PrefixpathType: Loại đường dẫn. Ở đây, Prefix nghĩa là bất kỳ yêu cầu nào bắt đầu với đường dẫn này sẽ được route đến backend.
            - **backend:** Cấu hình backend cho đường dẫn.
              - **service:** Tên service mà Ingress sẽ route traffic vào.
              - **port:** Port của service mà Ingress sẽ route traffic vào.
              - **number:** Số port của service mà Ingress sẽ route traffic vào. Ở đây, cả hai service đều lắng nghe trên port 80.

Tiến hành deploy file cấu hình Ingress:

      kubectl apply -f ingress.yaml

![Overview](/fcj-ss2-workshop-002/images/19.png)

Kiểm tra xem Ingress đã được tạo chưa:

      kubectl get ingress

![Overview](/fcj-ss2-workshop-002/images/20.png)

Như vậy, chúng ta đã tạo Ingress để route traffic bằng path.

### 4. Kiểm tra kết quả

Đầu tiên các bạn thấy thông tin IP của máy host:

      ifconfig

Ở đây thông tin IP của máy host mình là: 192.168.1.4

Để kiểm tra kết quả, chúng ta cần thêm 2 dòng vào file `hosts`, hiện tại mình đang sử dụng hệ điều hành Ubuntu nên file `hosts` nằm ở đường dẫn `/etc/hosts`:

      sudo nano /etc/hosts

Thêm 2 dòng sau vào file `hosts`:

    192.168.1.4 example.com

![Overview](/fcj-ss2-workshop-002/images/21.png)

Tiếp theo, mở trình duyệt và truy cập vào 2 domain `example.com/service1` và `example.com/service2`:

![Overview](/fcj-ss2-workshop-002/images/22.png)
![Overview](/fcj-ss2-workshop-002/images/23.png)

Như vậy, chúng ta đã sử dụng Ingress để route traffic bằng path.

