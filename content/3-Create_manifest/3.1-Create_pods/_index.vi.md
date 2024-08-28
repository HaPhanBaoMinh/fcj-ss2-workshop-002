---
title : "Create first pods"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
---

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/01.png)

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/02.png)

- **apiVersion: v1**: Khai báo Kubernetes API version mà chúng ta sử dụng.

- **kind: Pod**: Khai báo file manifest này sẽ tạo Pod object.

- **metadata**: metadata của Pod, ở đây mình khai báo **name** và **labels** của Pod. **labels** của pod sẽ có nhiệm vụ trong việc đánh dấu pod này sẽ thuộc service nào.

- **spec**: Đây là phần cấu hình pod của chúng ta

    - **containers**: Đây là một array các object chứa thông tin của các container chạy trong pod. Trong file của chúng ta hiện chỉ có 1 container nginx

        - **name: nginx**: Chúng ta đặt tên của container là nginx

        - **image: nginx:latest**: Thông tin docker images mà chúng ta sẽ sử dụng 

        - **ports**: 
             - **containerPort: 80**: Container sẽ lắng nghe trên cổng 80 để xử lý các kết nối HTTP.

### Apply manifest file

    kubectl apply -f ./pods.yaml

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/03.png)

Chúng ta có thể kiểm tra trạng thái pods của chúng ta bằng cách, các bạn có thể thấy pods của chúng ta đã vào trạng thái **Running** được 60s. Vậy là chúng ta đã hoàn thành xong bước đầu tiên.

    kubectl get pod

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/04.png)