---
title : "Tiến hành cài đặt Ingress Controller"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

Trong bài viết này, tôi sử dụng MicroK8s để cài đặt Ingress Controller, và sử dụng Nginx Ingress Controller làm ví dụ.

### 1. Cài đặt Ingress Controller bằng Add-on
Phần ingress này nằm trong phần Add-on của MicroK8s, nên việc cài đặt khá đơn giản.

        microk8s enable ingress

Sau khi cài đặt xong, chúng ta sẽ thấy một Pod mới được tạo ra:

![Overview](/fcj-ss2-workshop-002/images/03.png)
![Overview](/fcj-ss2-workshop-002/images/04.png)

Tuy nhiên sau đây tôi sẽ hướng dẫn các bạn cách cài đặt Ingress Controller bằng cách sử dụng Helm.
Phòng trường hợp bạn không sử dụng MicroK8s hoặc muốn tùy chỉnh nhiều hơn.

### 2. Cài đặt Ingress Controller bằng Helm

Đầu tiên tôi sẽ disable Add-on Ingress trước:

        microk8s disable ingress

![Overview](/fcj-ss2-workshop-002/images/05.png)

Tiếp theo, chúng ta sẽ cài đặt Helm:

        sudo snap install helm --classic

![Overview](/fcj-ss2-workshop-002/images/06.png)

Sau khi cài đặt xong, chúng ta sẽ add Helm repository của Nginx Ingress Controller:

        helm repo add nginx-stable https://helm.nginx.com/stable
        helm repo update

Tiếp theo, chúng ta sẽ cài đặt Nginx Ingress Controller:

        helm install nginx-ingress ingress-nginx/ingress-nginx