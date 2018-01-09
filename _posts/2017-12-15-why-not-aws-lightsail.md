---
layout: post
published: true
title: Why we switched from AWS Lightsail to EC2 for Gitlab
imagefeature: blog/aws-lightsail-create-gitlab.png
mathjax: false
featured: true
comments: false
description: AWS Lightsail vs AWS EC2
categories: 
  - aws
tags: ec2 aws lightsail vpc
canonical: https://www.transfon.com/blog/Lightsail-vs-EC2-Gitlab
---

Gitlab can do Continuous Integration, Continuous Delivery, and Continuous Deployment within the same web interface. You can host Gitlab CE yourself on your own servers or in a container or on the cloud providers for free.

AWS Lightsail is a new product from AWS, it as simple as digitalocean or linode, one click to setup Gitlab CE.

If you have a large website and looking for managed cloud service please check: <a href="https://www.transfon.com/services/managed-service">Transfon managed cloud service</a>.

<p style="text-align: center;"><img src="https://www.devopszen.com/images/blog/aws-lightsail-create-gitlab.png" alt="AWS Lightsail - Gitlab"/></p>

AWS Lightsail provides the fixed public IP which can be binded on a Lightsail instance. So when you modify the Lightsail instance the public IP will not change and you don't have to modify the DNS records which is good.

<p style="text-align: center;"><img src="https://www.devopszen.com/images/blog/lightsail-fixed-public-ip.png" alt="AWS Lightsail Networking and fixed IP"/></p>

There is a private IP of the instance similar to AWS EC2, which is using the CIDR 172.26.0.0/16.

The firewall is very simple, you can only control the ports connectivity. It is not allowed to block IP or whitelist IP. You can only do this inside the instance with iptables.

<p style="text-align: center;"><img src="https://www.devopszen.com/images/blog/lightsail-private-ip-firewall.png" alt="AWS Lightsail Networking and private IP"/></p>

The private subnet gave me hope to connect with and communicate with the existed AWS VPC. Then we can see there is an advanced feature called VPC peering at the Lightsail settings menu. It is just a on/off button for VPC peering.

<p style="text-align: center;"><img src="https://www.devopszen.com/images/blog/lightsail-vs-ec2-vpc-peering.png" alt="AWS Lightsail VPC peering"/></p>

VPC peering only enables the Two-way communication between 2 VPC, and it is not possible to communication via a 'middle man' VPC.

So the problem is you can only do VPC peering from AWS Lightsail VPC to the 'default' AWS VPC. We can't communite with the other custom VPC by default without setting up a proxy. Plus using the 'default' VPC is not a best practice.

<p style="text-align: center;"><img src="https://www.devopszen.com/images/blog/aws-ec2-gitlab-instance-marketplace.png" alt="AWS EC2 marketplace - Gitlab"/></p>

So, it is better to launch the Gitlab instance inside your existed VPC with a marketplace instance which is providing the same features.

