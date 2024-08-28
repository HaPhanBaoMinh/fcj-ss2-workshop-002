---
title : "Deployment"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.3 </b> "
---

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/15.png)

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/16.png)

- **apiVersion: v1**: Declares the Kubernetes API version that we are using.

- **kind: Deployment**: Declares that this manifest file will create a Deployment object. A Deployment helps manage the rollout and updates of ReplicaSets.

- **metadata**: Metadata of the Deployment; here we declare the name and labels of the Deployment.

    - **name: nginx-deployment**: The name of the Deployment is nginx-deployment.

    - **labels**: 

        - **app: nginx**: This is a label that the Deployment uses to manage other objects like ReplicaSets.

- **spec**:

    - **replicas: 2**: This section specifies the number of Pod replicas that the Deployment must maintain. The Deployment will ensure that there are always 2 Pods running.

    - **selector**:

        - **matchLabels**:

            - **app: nginx**: This section configures the Deployment to manage Pods with the label **app: nginx**.

        - **template**: This can be considered the blueprint for the Pods that the Deployment will create.

            - **metadata**:

                - **labels**:

                    - **app: nginx**: Pods will have this label, matching the selector above. This ensures that the Deployment will manage these Pods.

            - **spec**:

                - **containers**: This section specifies the containers that will run inside each Pod.

                    - **name: nginx-pod-with-deployment**: The name of the container is nginx-pod-with-deployment.

                    - **image: nginx:latest**: The image to be used is **nginx:latest**.

                    - **ports**:

                        - **containerPort: 80**: The container will listen on port 80 to handle HTTP connections.

The main difference between a Deployment and a ReplicaSet is that a Deployment provides more advanced features, such as rollout updates, rollbacks, and managing ReplicaSets. I will write a separate workshop to introduce this part.

### Apply manifest file

    kubectl apply -f ./deployment.yaml

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/17.png)

We can check the status of the Deployment by using:

    kubectl get deployment

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/18.png)

As we can see, there is currently 1 Deployment created and managed by this Deployment.

Next, let's check the pods and ReplicaSets created from this Deployment.

    kubectl get pod

    kubectl get replicaset

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/19.png)

As you can see, there are currently 2 pods created and 1 ReplicaSet created and managed by this Deployment.

Okay, so we have completed 2 out of 3. After we have created the Deployment, how can we use the resources we have created? Let's move on to the next step!
