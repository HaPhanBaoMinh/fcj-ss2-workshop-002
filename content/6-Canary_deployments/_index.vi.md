---
title : "Cấu hình Canary deployments"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

Trong bài viết này, tôi sẽ hướng dẫn các bạn cách triển khai Canary Deployments Ingress.

### 1. Canary Deployments là gì?

Canary Deployments là một phương pháp triển khai phần mềm mới một cách an toàn và kiểm soát. Phương pháp này cho phép bạn triển khai một phiên bản mới của ứng dụng và chỉ chuyển một phần nhỏ lưu lượng truy cập tới phiên bản mới.      Điều này giúp bạn kiểm tra phiên bản mới trước khi triển khai cho tất cả người dùng.

![Overview](/fcj-ss2-workshop-002/images/24.png)

### 2. Cấu hình Canary Deployments cho ingress

Ok chúng ta sẽ tái sử dụng lại 2 service ở phần trước.

Mình sẽ lấy ví dụ service 1 là phiên bản cũ và service 2 là phiên bản mới.

Chúng ta có file cấu hình Ingress như sau:

![Overview](/fcj-ss2-workshop-002/images/25.png)

Ở đây mình sẽ route 80% traffic vào service 1 và 20% traffic vào service 2

Tiến hành deploy file cấu hình Ingress:

        kubectl apply -f ingress.yaml

![Overview](/fcj-ss2-workshop-002/images/26.png)

### 4. Kiểm tra kết quả

Đầu tiên các bạn thấy thông tin IP của máy host:

      ifconfig

Ở đây thông tin IP của máy host mình là: 192.168.1.4

Để kiểm tra kết quả, chúng ta cần thêm 2 dòng vào file `hosts`, hiện tại mình đang sử dụng hệ điều hành Ubuntu nên file `hosts` nằm ở đường dẫn `/etc/hosts`:

      sudo nano /etc/hosts

Thêm 2 dòng sau vào file `hosts`:

    192.168.1.4 canary.example.com


Tiếp theo, mở trình duyệt và truy cập vào domain `canary.example.com`

![Overview](/fcj-ss2-workshop-002/images/27.png)
![Overview](/fcj-ss2-workshop-002/images/28.png)

Như vậy, chúng ta đã cấu hình Canary Deployments Ingress thành công với traffic 80% vào service 1 và 20% vào service 2.
