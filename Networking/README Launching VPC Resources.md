<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-ec2)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## Launching VPC Resources

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

VPC (Virtual Private Cloud) is a virtual network in AWS that you define.
It’s logically isolated from other networks in the AWS cloud.
You control IP address ranges, subnets, route tables, network gateways, and security settings.

### How I used Amazon VPC in this project

I used Amazon VPC to create an isolated network for my project. I set up public and private subnets, attached an Internet Gateway for the public subnet, configured route tables, and launched EC2 instances in the appropriate subnets with security groups controlling their access.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how quickly the VPC’s automatic setup could create subnets, route tables, and an Internet Gateway for me. It made configuring the network much faster than I anticipated.

### This project took me...

This project took me 1 hour. 

---

## Setting Up Direct VM Access

When AWS says “directly access your EC2 instance”, it means you connect to the instance without going through another system or service first.

### SSH is a key method for directly accessing a VM

SSH (Secure Shell) is a protocol that lets you securely log in and run commands on a remote machine — like your Linux EC2 instance.

### To enable direct access, I set up key pairs

In AWS, a key pair is used for securely connecting to your EC2 instances. It’s basically a set of two cryptographic keys:

Public key → AWS stores this on your instance.

Private key (.pem file) → You download and keep this on your computer.

When you create a key pair in AWS, you can choose the format for the private key:

.pem (Privacy Enhanced Mail)
Base64 encoded text format.
Default format for Linux/macOS.
Used with ssh -i my-key.pem.

---

## Launching a public server

From the EC2 Console (Instance > Networking tab):
You can modify:
Elastic IP → attach or detach.
Network interfaces (ENIs) → add or remove.
Security groups → adjust inbound/outbound rules.
Source/Dest. check → disable if needed (e.g., for NAT instance).
At the Subnet / VPC Level:
Change whether the subnet auto-assigns public IPs.
Edit the route table (e.g., route to Internet Gateway for internet access).
Modify Network ACLs.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

When you set up public and private servers (instances), they usually serve different purposes — so they should not have identical security rules.

My private server’s security group allows traffic only from the separate security group I created for my public server. This ensures that the private server can be accessed by the public server while remaining inaccessible directly from the internet.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I created a new VPC using the automatic setup in the ‘VPC and more’ tab, which automatically assigned subnets, a route table, and an Internet Gateway. I then created security groups for my public and private servers and launched the instances in the respective subnets.

A VPC resource map is basically a visual or logical overview of all the resources inside your VPC. It helps you see how everything is connected and organized.

VPCs are isolated from each other
Each VPC is a virtual network within AWS.
They don’t share routing or traffic unless you explicitly connect them (e.g., VPC Peering).
No IP conflict as long as they’re not connected

Because VPCs are isolated, the same IP ranges can exist in different VPCs without issues.

Example: Both VPC-A and VPC-B can use 10.0.0.0/16 even though they overlap.

IP conflicts occur only if you try to connect them

If you later create a VPC peering or Transit Gateway connection, AWS won’t allow overlapping CIDR blocks.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

Theoretically, the number of public subnets is limited by your VPC CIDR and subnet sizes.

Practically, AWS allows up to 200 subnets per VPC by default, all of which can be public if routed through an Internet Gateway.

NAT = Network Address Translation.

A NAT Gateway allows instances in private subnets to access the internet without exposing their private IP addresses.

It translates the private IP of the instance to the NAT Gateway’s public IP for outgoing traffic.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-ec2_8ee57662)

---

---
