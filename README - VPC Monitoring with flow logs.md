<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-monitoring)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## VPC Monitoring with Flow Logs

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a private, isolated section of the AWS cloud where you can launch AWS resources like EC2 instances, RDS databases, and more.

### How I used Amazon VPC in this project

Create public and private subnets for different EC2 instances.

Assign security groups to control which traffic is allowed between instances.

Set up a VPC peering connection to enable communication between two separate VPCs.

Use flow logs to monitor traffic and troubleshoot connectivity issues.

### One thing I didn't expect in this project was...

One thing I didn’t expect was how strict security group and NACL rules can block traffic even when instances are in the same VPC.

I assumed private IPs would automatically communicate, but I had to carefully adjust inbound/outbound rules and routing to make the ping and other connections work.

It showed me that network security and routing are just as important as launching the instances.

### This project took me...

This project took me 1 hour. 

---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will Create two VPCs.

### Step 2 - Launch EC2 instances

In this step, I will Launch an EC2 instance in each VPC, so we can use them to test your VPC peering connection later.

### Step 3 - Set up Logs

1.Set up a way to track all inbound and outbound network traffic.
2.Set up a space that stores all of these records.


### Step 4 - Set IAM permissions for Logs

Give VPC Flow Logs the permission to write logs and send them to CloudWatch.

Finish setting up your subnet's flow log.

---

## Multi-VPC Architecture

I started my project by launching 2 public subnets. 

Each VPC must have a unique IPv4 CIDR block so the IP addresses of their resources don't overlap. Having overlapping IP addresses could cause routing conflicts and connectivity issues!

### I also launched EC2 instances in each subnet

I allowed ICMP (for ping tests) and TCP (for SSH/connection) traffic in the EC2 security group rules.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are like a diary for your computer systems. They record everything that happens, from users logging in to errors popping up. It's the go-to place to understand what's going on with your systems, troubleshoot problems, and keep an eye on who’s doing what.

Think of a log group as a big folder in AWS where you keep related logs together. Usually, logs from the same source or application will go into the same log group, BUT logs are also region-specific. This means log data gets created and saved in the region it was created, although you can use CloudWatch dashboards to bring together logs from different regions.

### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

VPC Flow Logs by default don't have the permission to record logs and store them in your CloudWatch log group. This policy makes sure that your VPC can now send log data to your log group. 

I’m creating an IAM role so that my AWS resources (like EC2, Lambda, or ECS) can securely access other AWS services without using hard-coded credentials. Roles provide temporary permissions that are safer and easier to manage.

A custom trust policy is a JSON document you attach to an IAM role that defines which principals (users, services, or accounts) are allowed to assume the role.

In short: it answers “Who can use this role?”.

For example, you can create a custom trust policy that lets only a specific AWS account, service (like EC2), or federated identity provider assume the role.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

Get Instance 1 to send test messages to Instance 2.

### Step 6 - Set up a peering connection

Set up a connection link between your VPCs.

### Step 7 - Analyze flow logs

Review the flow logs recorded aboout VPC 1's public subnet.

Analyse the flow logs to get some tasty insights

---

## Connectivity troubleshooting

EC2 instance started sending ICMP echo requests (ping) to 10.2.4.144, but it hasn’t received any replies yet.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-monitoring_99d4ba42)

Receiving ping replies from the public IPv4 address means Instance 2 is correctly configured to respond to ping requests, and Instance 1 can actually communicate with Instance 2 if it traffic goes across the public internet.

---

## Connectivity troubleshooting

No route between the two subnets/VPCs (e.g., no VPC peering, transit gateway, or routing entry).

### To solve this, I set up a peering connection between my VPCs

Traffic in VPC 1 won't know how to get to resources in VPC 2 without a route in your route table. You need to set up a route that directs traffic bound for VPC 2 to the peering connection you've set up.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

The network path is working between the two instances.

Routing, security groups, and NACLs are correctly configured to allow ICMP.

The destination instance is up and reachable on its private IP.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Version – Format version of the log.

Account ID – AWS account that owns the resource.

Interface ID – The ENI (Elastic Network Interface) where traffic was captured.

Source address & port – IP and port sending the traffic.

Destination address & port – IP and port receiving the traffic.

Protocol – Network protocol (e.g., TCP=6, UDP=17, ICMP=1).

Packets & Bytes – Number of packets and bytes transferred.

Start & End time – Timestamps for the flow.

Action – ACCEPT or REJECT, depending on security group/NACL.

Log status – Tells if the record was logged successfully.

Your flow log screenshot would tell you details about the traffic, such as:

Which IP/port pair communicated (source and destination).

Which protocol was used (TCP, UDP, ICMP).

How much traffic was sent (packets and bytes).

When the traffic happened (start and end time).

Whether it was allowed or denied (ACCEPT/REJECT).

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Logs Insights is an Amazon CloudWatch feature that lets you search, analyze, and visualize log data quickly using a query language.

I ran the query "Top 10 byte transfers by source and destination IP addresses" 

What it does:

fields srcAddr, dstAddr, bytes → Selects source IP, destination IP, and byte count.

stats sum(bytes) as totalBytes by srcAddr, dstAddr → Aggregates total bytes transferred between each pair.

sort totalBytes desc → Orders from highest to lowest traffic.

limit 10 → Shows only the top 10 flows.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-monitoring_3e1e79a1)

---

---
