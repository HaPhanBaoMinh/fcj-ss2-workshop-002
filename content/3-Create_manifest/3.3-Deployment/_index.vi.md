---
title : "Deployment"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.3 </b> "
---

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/15.png)

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/16.png)

- **apiVersion: v1**: Khai báo Kubernetes API version mà chúng ta sử dụng.

- **kind: Deployment**: Khai báo file manifest này sẽ tạo Deployment object. Deployment giúp quản lý việc triển khai và cập nhật của ReplicaSet.

- **metadata**: metadata của Deployment, ở đây mình khai báo name và labels của Deployment.

    - **name: nginx-deployment**: Tên của Deployment là nginx-deployment.

    - **labels**: 

        - **app: nginx**: Đây là một nhãn mà Deployment sử dụng để quản lý các đối tượng khác như ReplicaSet.

- **spec**:

    - **replicas: 2**: Phần này xác định số lượng bản sao của Pod mà Deployment phải duy trì. Deployment sẽ đảm bảo luôn có 2 Pod đang chạy.

    - **selector**:

        - **matchLabels**:

            - **app: nginx**: Phần này cấu hình Deployment biết sẽ quản lý các Pod có label là **app: nginx**.

        - **template**: Đây có thể coi là bản thiết kế cho các Pod mà Deployment sẽ tạo ra.

            - **metadata**:

                - **labels**:

                    - **app: nginx**: Pod sẽ có label này, khớp với selector ở trên. Đảm bảo rằng Deployment sẽ quản lý các Pod này.

            - **spec**:

                - **containers**: Phần này xác định các container sẽ chạy bên trong mỗi Pod.

                    - **name: nginx-pod-with-deployment**: Tên của container là nginx-pod-with-deployment.

                    - **image: nginx:latest**:  Image sẽ sử dụng là **nginx:latest**.

                    - **ports**:

                        - **containerPort: 80**: Container sẽ lắng nghe trên cổng 80 để xử lý các kết nối HTTP.

Khác biệt chính giữa Deployment và ReplicaSet là Deployment cung cấp nhiều tính năng cao cấp hơn, như khả năng cập nhật rollout, rollback và quản lý ReplicaSet. Phần này mình sẽ viết hẳn 1 Workshop để giới thiệu về phần này.

### Apply manifest file

    kubectl apply -f ./deployment.yaml

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/17.png)

Chúng ta có thể kiểm tra trạng thái Deployment bằng cách:

    kubectl get deployment

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/18.png)

Như chúng ta có thể thấy hiện tại đã có 1 Deployment được tạo và được quản lý bởi Deployment này.

Tiếp theo chúng ta hãy kiểm tra các pods và replicaSet được tạo ra từ Deployment này.

    kubectl get pod

    kubectl get replicaset

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/19.png)

Nhu các bạn có thể thấy hiện tại đã có 2 pods được tạo và 1 replicaSet được tạo và được quản lý bởi Deployment này.

Okay vậy là chúng ta đã đi được 2/3. Sau khi chúng ta đã tạo xong Deployment, vậy làm sao để chúng ta có thể sử dụng các tài nguyên mà chúng ta đã tạo ra. Mời các bạn qua bước tiếp theo nhé.


