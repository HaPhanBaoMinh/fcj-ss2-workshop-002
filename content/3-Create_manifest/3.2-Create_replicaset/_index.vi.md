---
title : "Create ReplicaSet"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/05.png)

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/06.png)

- **apiVersion: v1**: Khai báo Kubernetes API version mà chúng ta sử dụng.

- **kind: ReplicaSet**: Khai báo file manifest này sẽ tạo ReplicaSet object.

- **metadata**: metadata của ReplicaSet, ở đây mình khai báo **name** và **labels** của ReplicaSet.

- **spec**:
    - **replicas: 2**: Phần này xác định số lượng bản sao của pod mà ReplicaSet phải duy trì. Ở đây, ReplicaSet phải đảm bảo luôn có 2 pod đang chạy.

- **selector**:
    - **matchLabels**:
        - **app: nginx**: Phần này cấu hình ReplicaSet biết sẽ quản lý các pod có label là app: **nginx**.

- **template**: Đây có thể coi là bản thiết kế cho các pod mà ReplicaSet sẽ tạo ra.
    - **metadata**:
        - **labels**:
            - **app: nginx**: Pod sẽ có label này, khớp với selector ở trên. Đảm bảo rằng ReplicaSet sẽ quản lý các pod này.

    - **spec**:

        - **containers**: Phần này xác định các container sẽ chạy bên trong mỗi pod.
            - **name: nginx-pod-with-replicaset**: Tên của container là nginx-pod-with-replicaset.
            - **image: nginx:latest**: Image sẽ sử dụng là nginx:latest.
            - **ports**:
                - **containerPort: 80**: Container sẽ lắng nghe trên cổng 80 để xử lý các kết nối HTTP.

### Apply manifest file

    kubectl apply -f ./replica-set.yaml

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/07.png)

Chúng ta có thể kiểm tra trạng thái replicaSet bằng cách:

    kubectl get replicaset 

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/14.png)

Như các bạn có thể thấy hiện tại đã có 2 pod được tạo và được quản lý bởi replicaSet này.

Chúng ta có thể kiểm tra trạng thái pods của chúng ta bằng cách.

    kubectl get pod

Nếu như đúng thì sẽ có tổng cộng 3 pod được tạo ra, 1 pod từ step trước chúng ta đã làm. và 2 pod sẽ được tạo từ ReplicaSet. Nhưng không! hãy nhìn xem. Chỉ có 1 pods mới được tạo ra, vì sao vậy ?

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/08.png)

Chúng ta hãy xem thông tin chi tiết của cả 2 pods này nhé


    kubectl describe pod nginx-pod

    kubectl describe pod nginx-replicaset-p7r9f

Hãy để ý phần **Labels** của cả 2 như sau:

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/09.png)

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/11.png)

Cả 2 đều có chung 1 **Labels** đồng nghĩa với việc pod mà chúng ta đã tạo ra từ step trước đã được quản lý cùng với pod mới bằng replicaSet của chúng ta vừa tạo.

Bây giờ chúng ta hãy test tính năng **self-healing** của relicaSet bằng cách thử xóa 1 pod xem chuyện gì sẽ xảy ra!

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/12.png)

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/13.png)

Như các bạn có thể thấy khi chúng ta xóa 1 pod thì ngay lập tức K8s tạo thêm cho chúng ta 1 pod mới, và nó đang trong trạng thái **ContainerCreating**. Việc này đảm bảo tính **HA** cho chúng ta, khi luôn đảm bảo có đủ số Pod chạy.

Tới đây thì cũng thấy được phần nào sự lợi hại của K8s rồi đúng không. Tuy nhiên nếu service chúng ta có version mới cần triển khai thì sao ? Mời các bạn đến với step số 3 nhé!