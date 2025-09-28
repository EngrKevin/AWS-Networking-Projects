<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a logically isolated virtual network in AWS where you can launch and manage your resources (like EC2, RDS, etc.). You control the IP address ranges, subnets, route tables, and network gateways.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create an isolated network environment for my resources. I set up subnets, route tables, and security groups, then established a VPC peering connection so instances in two different VPCs could communicate privately. I validated the setup using ping tests and updated inbound rules to allow ICMP traffic between the VPCs.


### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was that creating the VPC peering connection alone wasn’t enough. I had to also update the route tables and security group rules in both VPCs before the instances could actually communicate. Without those changes, the peering connection existed but traffic couldn’t flow.

### This project took me...

This project took me 40 minutes. 

---

## In the first part of my project...

### Step 1 - Set up my VPC

Create two VPCs from scratch!

Use the visual VPC resource map 

### Step 2 - Create a Peering Connection

In this step, I will Create a Peering Connection between two vpc. 

### Step 3 - Update Route Tables

Set up a way for traffic coming from VPC 1 to get to VPC 2.

Set up a way for traffic coming from VPC 2 to get to VPC 1.

### Step 4 - Launch EC2 Instances

In this step, I will Launch an EC2 instance in each VPC, so we can use them to test your VPC peering connection later.



---

## Multi-VPC Architecture

I started my project by launching 2 VPCs. 1 subnet for each VPC. 

Each VPC must have a unique IPv4 CIDR block so the IP addresses of their resources don't overlap. Having overlapping IP addresses could cause routing conflicts and connectivity issues. 

### I also launched 2 EC2 instances

With EC2 Instance Connect, AWS manages a key pair for us! We don't need to manage key pairs ourselves. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a networking connection between two Virtual Private Clouds (VPCs) that allows them to communicate privately using private IPv4 or IPv6 addresses. Essentially, it’s like creating a direct, private link between two separate networks in AWS.

VPC peering connections exist to enable secure and private communication between separate VPC networks without exposing traffic to the public internet. Essentially, they solve the problem of needing multiple isolated networks to “talk” to each other safely.


In a VPC peering connection, there are always two parties involved: the Requester and the Accepter. These roles define who initiates the connection and who approves it.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because it has to know its way going to VPC 1 and VPC 2. 

The new route I added to my VPCs’ route tables was the CIDR block of the peer VPC, pointing to the VPC peering connection.

In VPC-A’s route table, I added a route to VPC-B’s CIDR block with the target set to the peering connection.

In VPC-B’s route table, I did the same but for VPC-A’s CIDR block.

This allows instances in both VPCs to send traffic to each other using private IP addresses.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

1. Use EC2 Instance Connect to connect to your first EC2 instance.

2. Fix a connection error.

### Step 6 - Connect to EC2 Instance 1

Use EC2 Instance Connect to connect to Instance 1 (one more time)!

Fix (another) error

### Step 7 - Test VPC Peering

Get Instance 1 to send test messages to Instance 2.

Solve connection errors until Instance 2 is able to send messages back.



---

## Troubleshooting Instance Connect

I’m using EC2 Instance Connect to securely connect to my EC2 instance without needing to manage SSH keys locally. It lets me use a temporary SSH key that AWS generates and pushes to the instance, which improves security and makes access easier from the AWS Management Console or CLI.

I was stopped from using EC2 Instance Connect as there was no public IPv4 address attached to my EC2 instance. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

An Elastic IP address (EIP) is a static, public IPv4 address in AWS that you can allocate to your account and associate with EC2 instances or other resources.

Elastic IP addresses solved the connection error by giving my EC2 instance a static public IP.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command ping 10.2.11.172.

A ping test validates VPC peering by checking if instances in the two VPCs can reach each other using their private IP addresses.

I updated my instance’s security group inbound rules by adding an ICMP rule (for ping) or the required port rule (like SSH on port 22 or HTTP on port 80) to allow traffic from the CIDR block of the peer VPC or from specific IPs.

For the ping test, I added an inbound rule that allowed ICMP traffic from the other VPC’s CIDR range.

For SSH/web access, I added inbound rules for the correct port and source.

This ensured that traffic from the peered VPC could reach my instance.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-peering_7a29d352)

---

---
