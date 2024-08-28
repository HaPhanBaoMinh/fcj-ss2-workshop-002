---
title : "Core Concepts"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 1. </b> "
---

![Overview](/fcj-ss2-workshop-001/images/1-Basic_concepts./03.png)

## 1. K8s là gì và tại sao chúng ta nên dùng nó ?

Khi bạn tìm kiếm câu hỏi này trên internet bạn có thể thấy rất nhiều các khái niệm và cách giải thích được nhắc đến. Dưới đây là cách giải thích của tôi về công nghệ này.

Tưởng tượng rằng trong một dự án xây dựng sẽ có nhiều các bộ phận đảm nhiệm các công việc khác nhau, ví dụ như: 

- Bộ phận xây dựng
- Bộ phận hậu cần
- Bộ phận sơn
- Bộ phận làm điện
- Bộ phận làm nước 

và người điều phối và đảm bảo các công việc này hoạt động một cách trơn tru và kịp tiến độ sẽ là **người chủ thầu**.

Trong trường hợp bộ phận xây dựng đang trễ tiến độ thì **người chủ thầu** phải tìm cách thêm tài nguyên có bộ phận này bằng cách tuyển thêm người, để đảm bỏa rằng công việc diễn ra đúng kế hoạch và không bị gián đoạn.

Trong trường hợp này có thể coi **K8s** là **người chủ thầu** trong trường hợp trên. **K8s** sẽ đóng vai trò như một người điều phối trong hệ thống, mỗi service trong hệ thống giống như một bộ phận trong dự án xây dựng đó. Khi một service có vấn đề (thiếu tài nguyên, app bị cash, ...) thì **K8s** sẽ có vai trò cung cấp thêm các "công nhân" bằng cách scale thêm các **Pod** để  xử lý. 

Ngoài ra còn có rất nhiều lợi ích khác từ việc sử dụng **K8s** trong việc triển khai. Các bạn có thể tham khảo thêm ở [video](https://www.youtube.com/watch?v=a2gfpZE8vXY).

## 2. Các Core Concepts trong K8s

- Control Plane
- Nodes
- Pod
- ReplicaSet
- Deployment
- Namespace
- Services
- Types of Services

## 3. Tài liệu tham khảo

- [Overview - kubernetes](https://kubernetes.io/docs/concepts/overview/)
- [Getting Started with K8s: Core Concepts](https://edgehog.blog/getting-started-with-k8s-core-concepts-135fb570462e)