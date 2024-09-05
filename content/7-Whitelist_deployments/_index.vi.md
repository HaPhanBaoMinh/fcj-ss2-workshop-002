---
title : "Cấu hình Ingress với IP Whitelist"
date :  "`r Sys.Date()`" 
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

Trong bài viết này, tôi sẽ hướng dẫn các bạn cách cấu hình Ingress với IP Whitelist.

### 1. IP Whitelist là gì?

IP Whitelist là một danh sách các địa chỉ IP được phép truy cập vào một dịch vụ hoặc một ứng dụng. Các IP không nằm trong danh sách này sẽ không thể truy cập vào dịch vụ hoặc ứng dụng đó.

Ứng dụng của chứng năng này là để bảo vệ dịch vụ hoặc ứng dụng khỏi các cuộc tấn công từ các IP không mong muốn. Hoặc giới hạn quyền truy cập vào dịch vụ hoặc ứng dụng với một số IP cụ thể như các IP nội bộ của công ty, ...

![Overview](/fcj-ss2-workshop-002/images/00.webp)

### 2. Cấu hình Ingress với IP Whitelist

Ok chúng ta sẽ tái sử dụng lại 2 service ở phần trước.

Mình sẽ lấy ví dụ service 1 là phiên bản cũ và service 2 là phiên bản mới.

Chúng ta sẽ cấu hình chỉ có IP `192,168.1.10` được truy cập vào service 2 thôi.

![Overview](/fcj-ss2-workshop-002/images/29.png)

Trong file cấu hình trên chúng ta route "service2.example.com" vào service 2, tuy nhiên chỉ có IP `192.168.1.10` được truy cập vào service 2. 

Tiến hành deploy file cấu hình Ingress:

        kubectl apply -f ingress.yaml

![Overview](/fcj-ss2-workshop-002/images/30.png)

### 4. Kiểm tra kết quả

Đầu tiên các bạn thấy thông tin IP của máy host:

      ifconfig

Ở đây thông tin IP của máy host mình là: 192.168.1.4

Để kiểm tra kết quả, chúng ta cần thêm 2 dòng vào file `hosts`, hiện tại mình đang sử dụng hệ điều hành Ubuntu nên file `hosts` nằm ở đường dẫn `/etc/hosts`:

      sudo nano /etc/hosts

Thêm 2 dòng sau vào file `hosts`:

    192.168.1.4 service2.example.com

Tiếp theo, mở trình duyệt và truy cập vào domain `service2.example.com` bằng chính máy host, và gặp thông báo lỗi `403 Forbidden`:

![Overview](/fcj-ss2-workshop-002/images/31.png)

Tiếp theo chúng ta sẽ thử truy cập vào domain `service2.example.com` bằng máy có IP `192.168.1.10`:

Hiện tại đây là máy với IP đúng với IP được whitelist:

![Overview](/fcj-ss2-workshop-002/images/32.png)

Ở đây tôi cũng phải cấu hình thông tin `/etc/hosts` như trên máy có IP `192.168.1.10`:

Sau có chúng ta tiến hành curl vào domain `service2.example.com`:

        curl service2.example.com

Kết quả trả về:

![Overview](/fcj-ss2-workshop-002/images/33.png)

Như vậy, chúng ta đã cấu hình Ingress với IP Whitelist thành công. Chỉ có IP `192.168.1.10` được truy cập vào service 2.