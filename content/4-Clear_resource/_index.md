---
title : "Clear Resource"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

After we have created the resources, you can delete them when you no longer need them. Alternatively, you can keep those resources for future Workshops.

### Deleting Resources

To delete a resource, we use the `kubectl delete` command with the following syntax:

    kubectl delete <resource_type> <resource_name>

For example, to delete a Deployment named `nginx-deployment`, we use the command:

    kubectl delete deployment nginx-deployment

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/25.png)

Check if the Deployment has been deleted:

    kubectl get deployment -A

![Overview](/fcj-ss2-workshop-001/images/2-Manifest/26.png)

As you can see, the Deployment `nginx-deployment` is no longer present.
