---
title : "Service"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 3.4 </b> "
---

### Introduction to Kubernetes Service

In Kubernetes, a **Service** is an object that defines how to connect and access Pods. Pods often have a short lifespan and can be replaced at any time. Therefore, a **Service** provides a stable access point (usually an IP address or DNS) to communicate with those Pods, regardless of whether the Pods are replaced or not.

### Service Exposure Types

Kubernetes provides three main types of exposure for Services:

1. **ClusterIP** (default): Creates an internal IP for the Service that can only be accessed within the cluster. This is the most common and simplest type of exposure.

2. **NodePort**: Opens a port on each Node to allow external access to the Service. NodePort maps a random (or predefined) port on each Node to the `port` of the Service.

3. **LoadBalancer**: Creates an external load balancer (typically from a cloud provider) and routes traffic from this load balancer to the Nodes in the cluster.

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/20.png)

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/21.png)

- **apiVersion: v1**: Declares the Kubernetes API version we are using. v1 is the API version for the Service object.

- **kind: Service**: Declares that this manifest file will create a Service object.

- **metadata**: Metadata of the Service, where the name and labels of the Service are declared.

    - **name**: nginx-service: The name of the Service is nginx-service.

    - **labels**:
        app: nginx: This label helps classify and manage objects in Kubernetes.

- **spec**:

    - **type: NodePort**: This section specifies that the Service will be exposed to the outside through a specific port on each Node in the cluster.

    - **selector**:

        - **app: nginx**: This section configures the Service to know which Pods with the label app: nginx it will manage and forward traffic to.

    - **ports**: Defines the ports that the Service will use to listen for and forward traffic.

        - **protocol: TCP**: The Service will use the TCP protocol.

        - **port: 80**: This is the port that the Service will listen for traffic from outside the cluster.

        - **targetPort: 80**: This is the port to which traffic will be forwarded inside the container.

We have now created a Service with the exposure type **NodePort**. This Service will open a port on each Node in the cluster to allow access to the Pods of the Deployment.

### Apply manifest file

    kubectl apply -f ./service.yaml

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/22.png)

Check the status of the Service:

    kubectl get svc 

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/23.png)

As we can see, we have created a Service with the exposure type NodePort. This Service will open a port on each Node in the cluster to allow access to the Pods of the Deployment.

In the image, the port that the Service will listen for traffic from outside the cluster is **31905**, and the port to which traffic will be forwarded inside the container is **80**.

Next, I will try to access this port to check if the Service is functioning correctly.

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/24.png)

As we can see, the Service is functioning as expected, and we have accessed the Pod through the Service.

Thus, through this article, you have learned how to create a Service in Kubernetes and how to expose the Service to the outside of the cluster. In the next article, I will guide you on how to use **Ingress** to manage traffic from outside into the cluster.
