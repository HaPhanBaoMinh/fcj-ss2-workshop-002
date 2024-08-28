---
title : "Create ReplicaSet"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/05.png)

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/06.png)

- **apiVersion: v1**: Declares the Kubernetes API version that we are using.

- **kind: ReplicaSet**: Declares that this manifest file will create a ReplicaSet object.

- **metadata**: Metadata of the ReplicaSet; here we declare the **name** and **labels** of the ReplicaSet.

- **spec**:
    - **replicas: 2**: This section specifies the number of pod replicas that the ReplicaSet must maintain. Here, the ReplicaSet must ensure that there are always 2 pods running.

- **selector**:
    - **matchLabels**:
        - **app: nginx**: This part configures the ReplicaSet to manage pods with the label app: **nginx**.

- **template**: This can be considered the blueprint for the pods that the ReplicaSet will create.
    - **metadata**:
        - **labels**:
            - **app: nginx**: Pods will have this label, matching the selector above. This ensures that the ReplicaSet will manage these pods.

    - **spec**:

        - **containers**: This section specifies the containers that will run inside each pod.
            - **name: nginx-pod-with-replicaset**: The name of the container is nginx-pod-with-replicaset.
            - **image: nginx:latest**: The image to be used is nginx:latest.
            - **ports**:
                - **containerPort: 80**: The container will listen on port 80 to handle HTTP connections.

### Apply manifest file

    kubectl apply -f ./replica-set.yaml

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/07.png)

We can check the status of the ReplicaSet by using:

    kubectl get replicaset 

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/14.png)

As you can see, there are currently 2 pods created and managed by this ReplicaSet.

We can check the status of our pods by using:

    kubectl get pod

If everything is correct, there should be a total of 3 pods created: 1 pod from the previous step we did, and 2 pods created by the ReplicaSet. But no! Look, only 1 new pod has been created. Why is that?

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/08.png)

Let's look at the detailed information of both pods:

    kubectl describe pod nginx-pod

    kubectl describe pod nginx-replicaset-p7r9f

Notice the **Labels** of both as follows:

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/09.png)

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/11.png)

Both have the same **Labels**, meaning that the pod we created from the previous step has been managed along with the new pod by our newly created ReplicaSet.

Now let's test the **self-healing** feature of the ReplicaSet by trying to delete one pod and see what happens!

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/12.png)

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/13.png)

As you can see, when we delete one pod, K8s immediately creates a new pod for us, and it is in the **ContainerCreating** state. This ensures **HA** for us, as it always guarantees enough pods are running.

At this point, you can see some of the advantages of K8s, right? However, what if our service has a new version that needs to be deployed? Let's move on to step 3!
