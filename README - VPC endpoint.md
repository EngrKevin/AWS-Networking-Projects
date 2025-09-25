<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Endpoints

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-endpoints)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## VPC Endpoints

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_09bcaa8a)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a private, isolated network in AWS where you can launch and manage resources like EC2 and RDS.

✅ Why it’s useful:

Gives full control over IP addresses, subnets, and routing.

Secures resources with security groups and network ACLs.

Enables private connections to on-premises networks or the internet.

Provides isolation and customization for your cloud environment.

### How I used Amazon VPC in this project

In today’s project, I created a VPC and an EC2 instance inside it, then used a VPC endpoint to securely connect the instance to an S3 bucket for uploading files.

### One thing I didn't expect in this project was...

One thing I didn’t expect was learning how to use a VPC endpoint to access S3 securely without going through the public internet.

### This project took me...

This project took me 1 hour. 

---

## In the first part of my project...

### Step 1 - Architecture set up

Create a VPC from scratch!

Launch an EC2 instance, which you'll connect to using EC2 Instance Connect later.

Set up an S3 bucket.



### Step 2 - Connect to EC2 instance

In this step, I will Connect directly to the EC2 instance.

### Step 3 - Set up access keys

Giving our EC2 instance access to our AWS environment.

### Step 4 - Interact with S3 bucket

Head back to your EC2 instance.

Get your EC2 instance to access your S3 bucket.

---

## Architecture set up

I started my project by launching a VPC and an EC2 in it.

I also set up S3 and uploaded two files. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_4334d777)

---

## Access keys

### Credentials

VPC and Subnet – so the EC2 instance has a network to run in.

Security Group – to control inbound/outbound traffic.

IAM Role with S3 permissions – to allow the EC2 instance to access S3 without using access keys.

S3 Bucket – where you store and manage the files.

Access keys are a pair of security credentials (Access Key ID and Secret Access Key) that allow programmatic access to AWS services through tools like the AWS CLI or SDKs, instead of logging in with a password.

A Secret Access Key is the confidential part of an AWS access key pair that, together with the Access Key ID, is used to securely sign programmatic requests to AWS services.

### Best practice

The best practice alternative to using access keys is to use IAM roles (with temporary security credentials), especially with services like EC2, Lambda, or AWS SSO. This avoids hardcoding long-term credentials and improves security.

---

## Connecting to my S3 bucket

aws s3 ls. 

The terminal responded with the s3 bucket i created. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_4334d778)

---

## Connecting to my S3 bucket

aws s3 ls s3://s3-bucket-kevin0987

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_4334d779)

---

## Uploading objects to S3

sudo touch /tmp/kevin.txt 

aws s3 cp /tmp/kevin.txt s3://s3-bucket-kevin0987

aws s3 ls s3://s3-bucket-kevin0987

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_3e1e79a2)

---

## In the second part of my project...

### Step 5 - Set up a Gateway

Set up a way for your VPC and S3 to communicate directly.

### Step 6 - Bucket policies

Limiting theS3 bucket access's to only traffic from the  endpoint.

### Step 7 - Update route tables

Test your VPC endpoint set up.
Troubleshoot a connectivity issue.


### Step 8 - Validate endpoint conection

Test your VPC endpoint set up (again).

Restrict your VPC's acccess to your AWS environment

---

## Setting up a Gateway

A gateway is a network device or service that connects two different networks, allowing traffic to flow between them. In AWS, for example, an Internet Gateway lets a VPC communicate with the internet.

### What are endpoints?

An endpoint is a network entry point that allows your AWS resources (like EC2) to connect to another service (like S3) privately and securely, without going through the public internet.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_09bcaa8a)

---

## Bucket policies

A bucket policy is a set of permissions attached to an S3 bucket that defines who can access the bucket and what actions they can perform (like read, write, or delete objects).

My bucket policy controls access to the S3 bucket, specifying who can read or write files and ensuring only authorized users or resources (like my EC2 instance) can interact with the bucket.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_7316a13d)

---

## Bucket policies

Policy denies all actions unless they come from your VPC endpoint. This means any attempt to access your bucket from other sources, including the AWS Management Console, is blocked!

I also had to update my route table because the routing was still in the internet gateway going to the s3 bucket and there was no route with the vpc endpoint. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_4ec7821f)

---

## Route table updates

1. Select Endpoints from the left hand navigation panel.
2. Select the checkbox next to your endpoint, and select Route tables.
3. Select Manage route tables.
4. Select the checkbox next to your public route table.
5. Select Modify route tables.

After updating my public subnet's route table, my terminal could return the the files that I uploaded in the s3 bucket. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_d116818e)

---

## Endpoint policies

An endpoint policy is a set of rules attached to an AWS VPC endpoint that controls which AWS resources and actions can be accessed through that endpoint. It’s like a permission policy specifically for traffic going through the endpoint.

I updated my endpoint's policy by changing the defauly allow to deny, I could see the effect of this right away, because I can not access my s3 via the instance connect. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-endpoints_3e1e79a3)

---

---
