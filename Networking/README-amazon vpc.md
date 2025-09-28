<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-vpc)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a logically isolated virtual network you create in AWS. It lets you define and control your own networking environment in the cloud, similar to running your own data center.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a subnet and connect an internet gateway to a Public VPC.

### One thing I didn't expect in this project was...

I didn’t expect how much networking configuration (like subnets, route tables, and security groups) would affect the project. It taught me the importance of planning VPC design early.

### This project took me...

This project took me 30 minutes. 

---

## Virtual Private Clouds (VPCs)

VPCs in AWS is a logically isolated network where you can launch AWS resources .

AWS creates a default VPC in every account so that new users can quickly launch and use resources (like EC2 instances) without needing to set up networking from scratch.

An IPv4 CIDR block is a way of writing an IP address range using Classless Inter-Domain Routing (CIDR) notation.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-vpc_2facf927)

---

## Subnets

Subnets  in AWS is a smaller network inside your VPC, created by dividing the VPC’s IP address range.

When you enable auto-assign public IPv4 address for a subnet, any EC2 instance launched in that subnet will instantly get a public IP address so you won't have to create one manually - a huge time saver!

A subnet is not considered a public subnet unless it has a route to the Internet Gateway (IGW) in its route table.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-vpc_157c4219)

---

## Internet gateways

An internet gateway connects your city (VPC) and the outside world (internet).

Attaching an internet gateway means resources in your VPC can now access the internet.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

---

---
