<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a service that lets you create your own isolated network within AWS. You can define your IP address range, subnets, route tables, and security settings.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create an isolated network for my resources. Specifically:

Created subnets – Set up a public subnet for servers that need internet access and a private subnet for internal servers.

Configured route tables – Ensured traffic from the public subnet could reach the internet via an Internet Gateway, while the private subnet stayed isolated.

Applied security – Used security groups and network ACLs to control inbound and outbound traffic for each server.

Connected resources securely – Deployed EC2 instances inside the VPC, ensuring private instances could communicate internally without exposing them to the public internet.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how quickly security settings like security groups and NACLs can block traffic.

Even if the VPC and subnets were set up correctly, a single misconfigured rule could prevent instances from communicating or accessing the internet. It really showed me that network security in the cloud requires careful attention, not just creating the network.

### This project took me...

This project took me 1 hour. 

---

## Connecting to an EC2 Instance

Connectivity is all about how well different parts of your network talk to each other and with external networks. It's essential because connectivity is how data flows smoothly across your network, powering everything from simple web hosting on the Internet to complex operations e.g. Netflix using over 100,000 EC2 instances to power its streaming platform. Solid connectivity is the backbone of any system that relies on network interactions, making every communication and operation reliable and efficient.

My first connectivity test was whether I could connect to my public server. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

Amazon EC2 Instance Connect is a feature that lets you securely connect to your EC2 instances using SSH, without needing to manage long-lived SSH keys.

Set up in the Inbound rule of Security group lacks the ssh rule. 

I fixed this error by adding ssh rule in the inbound rule of Security Group. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a basic network command used to test if one computer can reach another over a network.

It sends a special message called an ICMP Echo Request to the target, and if the target replies with an ICMP Echo Reply, you know:

The target is up (alive).

The network path between them works.

ping 10.0.2.90

The first ping reply you saw means:

Your public instance could reach the private instance at least once.

That confirms:

Routing between subnets works (the packet reached the private instance).

The private instance replied with an ICMP Echo Reply.

So, network path and instance are both alive. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

First ping reply proved the route table and subnet association were correct.

The failure after one reply pointed to stateless filtering → likely the NACL.

Remember: NACLs are stateless, so both inbound and outbound rules must be set.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

curl is a command-line tool and library used to transfer data to or from a server using various protocols such as HTTP, HTTPS, FTP, SFTP, and more. It’s extremely popular for testing APIs, downloading files, or interacting with web services from the terminal or scripts.

I used curl because it’s one of the simplest and most direct ways to interact with a server or API from the command line.

### Ping vs Curl

ping → checks if a server is reachable and measures response time (uses ICMP).

curl → fetches data from a server or API (uses HTTP, HTTPS, FTP, etc.).

---

## Connectivity to the Internet

curl example.com
curl https://learn.nextwork.org/projects/aws-host-a-website-on-s3



![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-connectivity_8ee57662)

---

---
