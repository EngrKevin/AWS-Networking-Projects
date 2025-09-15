<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a virtual network in AWS that you control completely. It lets you define:

IP address ranges (subnets)

Route tables (how traffic flows)

Network ACLs and security groups (who can access what)

Internet or VPN access

### How I used Amazon VPC in this project

Created a VPC with a defined IP range for the project.

Set up public and private subnets:

Public subnet for internet-facing resources (like a web server or NAT Gateway).

Private subnet for internal resources (like a database) that shouldn’t be directly exposed.

Configured route tables to control traffic:

Public subnet routes traffic to the Internet Gateway.

Private subnet routes outbound traffic through a NAT Gateway.

Applied security groups and NACLs to control inbound/outbound traffic at the instance and subnet level.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how carefully subnet routing and NACLs need to be planned. Even small misconfigurations can block traffic completely, making it tricky to debug connectivity between public and private subnets.

### This project took me...

This project took me 40 minutes. 

---

## Private vs Public Subnets

Public subnet → has a route to an Internet Gateway. Instances can get public IPs and talk directly to the internet.

Private subnet → no direct route to the internet. Instances are isolated and use a NAT (or stay internal only).

They let you keep resources (like databases, app servers, or internal tools) hidden from the public internet, reducing the attack surface. Those resources can still talk out to the internet (via a NAT) if needed, but they can’t be reached directly from outside.

Your public and private subnets cannot share the same route table if you want them to behave differently.

Public subnets need a route to the Internet Gateway (IGW).

Private subnets must not have that IGW route (otherwise they’d also be public).

So while they can share the same VPC, NACLs, or security groups, they must use different route tables to stay truly “public” vs “private.”

Would you like me to also list what they can share

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, when you create a new subnet in a VPC, it’s associated with the main route table of that VPC.

 Since the main route table has no Internet Gateway (IGW) route by default, the subnet is effectively a private subnet until you add a route to an IGW.

For a public subnet, you create a new route table with a route to the Internet Gateway (IGW).

For a private subnet, you might create a new route table with a route to a NAT Gateway (so instances can go out but not be reached from outside).

Internal VPC traffic → communication with other subnets in the same VPC (local route).

Optional outbound traffic → if you add a route to a NAT Gateway/Instance in a public subnet, instances can reach the internet (for updates, patches, etc.).

No direct inbound/outbound internet traffic → there’s no route to the Internet Gateway (IGW).

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, every subnet in a VPC — whether public or private — is automatically associated with the default Network ACL of the VPC (unless you explicitly associate it with a custom one).

So, your private subnet’s route still uses the default NACL by default.

You set up a new network ACL (NACL) when you want an extra layer of subnet-level security that’s different from the default.

In a new custom NACL (for a private subnet), the inbound and outbound rules are usually set based on what traffic you want to allow. By default, a new NACL starts with no rules, so everything is denied until you add rules.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-private_1ed2cb07)

---

---
