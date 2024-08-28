---
title: "Deployment"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: "<b> 1.5 </b>"
---

![Overview](/fcj-ss2-workshop-002/images/1-Basic_concepts./06.png)

## 1. Deployment

When a service or application is deployed, it will be continuously updated with new versions. When updating new versions for containers, we need an automated update mechanism instead of manually updating each service, which can be especially difficult when our service has dozens or even hundreds of containers. The Deployment object helps us handle these issues.

Additionally, Deployment provides rollback mechanisms if the new version encounters issues and can manage Deployment versions, allowing us to roll back to a specific version if needed.

