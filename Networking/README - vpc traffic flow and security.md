<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-security)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## VPC Traffic Flow and Security

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

ChatGPT said:

Amazon VPC (Virtual Private Cloud) is a logically isolated virtual network within AWS where you can launch and manage your cloud resources, such as EC2 instances, databases, and load balancers. It lets you control networking just like in an on-premises data center.

### How I used Amazon VPC in this project

ChatGPT said:

In today’s project, I used Amazon VPC to create a secure, isolated network environment for our cloud resources.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how much planning and coordination was required for networking components.

For example:

Ensuring the CIDR blocks didn’t overlap between VPCs and subnets.

Properly configuring route tables, Internet Gateways, and security groups so resources could communicate without exposing them unnecessarily.

Managing resources across multiple regions (like Tokyo and Singapore) to avoid confusion.

### This project took me...

This project took me 1 hour. 

---

## Route tables

A route table in AWS is a set of rules (routes) that control where network traffic goes within your VPC.

You need a route table to make a subnet public because it tells the subnet how to send traffic to the internet.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Destination → Where the traffic is going
Target → Where the traffic should go

Destination: 0.0.0.0/0 → means all internet traffic

Target: igw-xxxxxxxx → the Internet Gateway attached to your VPC

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-security_0a07b191)

---

## Security groups

A security group in AWS is a virtual firewall that controls inbound and outbound traffic for your resources (like EC2 instances).

### Inbound vs Outbound rules

An inbound rule in a security group specifies what traffic is allowed to enter your resources (like an EC2 instance).

An outbound rule in a security group specifies what traffic is allowed to leave your resources (like an EC2 instance).

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACL (Access Control List) in AWS is another layer of security for your VPC that controls traffic at the subnet level, rather than the instance level like security groups.

### Security groups vs. network ACLs

Security Group - Instance level
NACL - Subnet level

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

For all default Network ACLs (NACLs) in AWS, the rules are very simple and allow all traffic by default. 

A custom Network ACL (NACL) in AWS gives you full control over what traffic is allowed or denied at the subnet level.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

I created additional... Instead of my usual region, I used  ap-northeast-2 and ap-southeast-1. 



EC2 Global View in AWS lets you see all your EC2 resources across multiple regions in a single interface.

You would use EC2 Global View when you want to see and manage your EC2 resources across multiple AWS regions in one place.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-security_b03ea6162)

---

---
