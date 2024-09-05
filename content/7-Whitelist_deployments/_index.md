---
title : "Configuring Ingress with IP Whitelist"
date :  "`r Sys.Date()`" 
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

In this article, I will guide you on how to configure Ingress with an IP Whitelist.

### 1. What is an IP Whitelist?

An IP Whitelist is a list of IP addresses that are allowed to access a service or application. IPs not on this list will not be able to access that service or application.

The purpose of this feature is to protect the service or application from attacks from unwanted IPs or to restrict access to specific IPs, such as internal company IPs.

![Overview](/images/00.webp)

### 2. Configuring Ingress with IP Whitelist

We will reuse the two services from the previous section.

I will take service 1 as the old version and service 2 as the new version.

We will configure access to service 2 so that only the IP `192.168.1.10` is allowed.

![Overview](/images/29.png)

In the configuration file above, we route "service2.example.com" to service 2, but only the IP `192.168.1.10` is allowed to access service 2.

Deploy the Ingress configuration file:

        kubectl apply -f ingress.yaml

![Overview](/images/30.png)

### 3. Check the Result

First, find the host machine's IP information:

      ifconfig

Here, the host's IP is: 192.168.1.4

To check the result, we need to add a line to the `hosts` file. Currently, I'm using Ubuntu, so the `hosts` file is located at `/etc/hosts`:

      sudo nano /etc/hosts

Add the following lines to the `hosts` file:

    192.168.1.4 service2.example.com

Next, open a browser and access the domain `service2.example.com` from the host machine. You will encounter a `403 Forbidden` error:

![Overview](/images/31.png)

Next, we will try to access the domain `service2.example.com` from a machine with the IP `192.168.1.10`:

Currently, this is the machine with the correct whitelisted IP:

![Overview](/images/32.png)

Here, I also need to configure the `/etc/hosts` file as on the machine with the IP `192.168.1.10`:

After that, we will proceed to curl the domain `service2.example.com`:

        curl service2.example.com

The response will be:

![Overview](/images/33.png)

Thus, we have successfully configured Ingress with an IP Whitelist, allowing only the IP `192.168.1.10` to access service 2.
