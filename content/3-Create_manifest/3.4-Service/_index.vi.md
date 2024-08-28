---
title : "Service"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 3.4 </b> "
---

### Giới Thiệu về Kubernetes Service

Trong Kubernetes, **Service** là một đối tượng giúp định nghĩa cách thức kết nối và truy cập tới các Pod. Các Pod thường có vòng đời ngắn ngủi và có thể bị thay thế bất cứ lúc nào. Vì vậy, một **Service** sẽ cung cấp một điểm truy cập ổn định (thường là một địa chỉ IP hoặc DNS) để giao tiếp với các Pod đó, bất kể các Pod bị thay thế hay không.

### Các Kiểu Expose Của Service

Kubernetes cung cấp ba loại expose chính cho Service:

1. **ClusterIP** (Mặc định): Tạo ra một IP nội bộ cho Service chỉ có thể truy cập được bên trong cluster. Đây là kiểu expose phổ biến nhất và đơn giản nhất.

2. **NodePort**: Mở một cổng trên mỗi Node để cho phép truy cập từ bên ngoài vào Service. NodePort sẽ map một cổng ngẫu nhiên (hoặc định sẵn) trên mỗi Node tới `port` của Service.

3. **LoadBalancer**: Tạo ra một load balancer bên ngoài (thường là từ nhà cung cấp cloud) và định tuyến traffic từ load balancer này đến các Node trong cluster.

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/20.png)

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/21.png)

- **apiVersion: v1**: Khai báo Kubernetes API version mà chúng ta sử dụng. v1 là API version cho đối tượng Service.

- **kind: Service**: Khai báo file manifest này sẽ tạo Service object.

- **metadata**: Metadata của Service, nơi khai báo name và labels của Service.

    - **name**: nginx-service: Tên của Service là nginx-service.

    - **labels**:
        app: nginx: Label này giúp phân loại và quản lý các đối tượng trong Kubernetes.

- **spec**:

    - **type: NodePort**: Phần này xác định Service sẽ được expose ra bên ngoài thông qua một cổng cụ thể trên mỗi Node trong cluster.

    - **selector**:

        - **app: nginx**: Phần này cấu hình Service biết sẽ quản lý và chuyển tiếp traffic tới các Pod có label app: nginx.

    - **ports**: Định nghĩa các cổng mà Service sẽ sử dụng để lắng nghe và chuyển tiếp traffic.

        - **protocol: TCP**: Service sẽ sử dụng giao thức TCP.

        - **port: 80**: Đây là cổng mà Service sẽ lắng nghe traffic từ bên ngoài cluster.

        - **targetPort: 80**: Đây là cổng mà traffic sẽ được chuyển tiếp tới bên trong container.

Hiện tại chúng ta đã tạo một Service với kiểu expose là **NodePort**, Service này sẽ mở một cổng trên mỗi Node trong cluster để cho phép truy cập vào Pod của Deployment.

### Apply manifest file

    kubectl apply -f ./service.yaml

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/22.png)

Kiểm tra trạng thái của Service

    kubectl get svc 

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/23.png)

Như vậy, chúng ta đã tạo một Service với kiểu expose là NodePort, Service này sẽ mở một cổng trên mỗi Node trong cluster để cho phép truy cập vào Pod của Deployment.

Trong hình thì cổng mà Service sẽ lắng nghe traffic từ bên ngoài cluster là **31905**, và cổng mà traffic sẽ được chuyển tiếp tới bên trong container là **80**.

Tiếp theo mình sẽ truy cập thử bằng port này để kiểm tra xem Service đã hoạt động đúng chưa.

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/24.png)

Như chúng ta có thể thấy, Service đã hoạt động đúng như mong đợi, chúng ta đã truy cập được vào Pod thông qua Service.

Vậy là qua bài viết này, bạn đã biết cách tạo một Service trong Kubernetes và cách expose Service ra bên ngoài cluster. Trong bài viết tiếp theo, mình sẽ hướng dẫn cách sử dụng **Ingress** để quản lý traffic từ bên ngoài vào trong cluster.