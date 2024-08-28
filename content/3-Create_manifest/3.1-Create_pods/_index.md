---
title: "Create first pods"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<b> 3.1 </b>"
---

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/01.png)

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/02.png)

- **apiVersion: v1**: Declares the Kubernetes API version we are using.

- **kind: Pod**: Declares that this manifest file will create a Pod object.

- **metadata**: Metadata for the Pod; here we declare the **name** and **labels** of the Pod. The **labels** of the Pod will serve to indicate which service this Pod belongs to.

- **spec**: This is the configuration section for our Pod.

    - **containers**: This is an array of objects containing information about the containers running in the Pod. In our file, we currently only have one container, nginx.

        - **name: nginx**: We name the container nginx.

        - **image: nginx:latest**: The Docker image information that we will use.

        - **ports**: 
            - **containerPort: 80**: The container will listen on port 80 to handle HTTP connections.

### Apply manifest file

    kubectl apply -f ./pods.yaml

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/03.png)

We can check the status of our pods by running the following command. You can see that our pod has been in the **Running** state for 60 seconds. So we have completed the first step.

    kubectl get pod

![Overview](/fcj-ss2-workshop-002/images/2-Manifest/04.png)

At this point, there's still nothing special, is there? It's not much different from running a container normally. So let’s move on to step two!
