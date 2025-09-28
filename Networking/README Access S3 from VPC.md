<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-s3)

**Author:** Kevin  
**Email:** kevinmatic93@gmail.com

---

## Access S3 from a VPC

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) is a logically isolated network in AWS where you can launch and manage your resources (like EC2, RDS, or Lambda) securely.

### How I used Amazon VPC in this project

In today’s project, I created a VPC and launched an EC2 instance inside it, then uploaded two files to an S3 bucket for storage.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was getting an error with the S3 bucket name because of invalid characters.

### This project took me...

This project took me 30 minutes. 

---

## In the first part of my project...

### Step 1 - Architecture set up

Create a VPC from scratch.

Launch an EC2 instance into your VPC.

### Step 2 - Connect to my EC2 instance

In this step, We are connecting directly to our EC2 instance.

### Step 3 - Set up access keys

Give your EC2 instance access to your AWS environment.

---

## Architecture set up

I started my project by launching a vpc and an ec2. 

created S3 bucket and uploaded two files in it. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

AWS CLI (Command Line Interface) is a tool that lets you manage AWS services and resources directly from your command line using commands instead of the AWS Management Console.

The first command I ran was aws s3 ls

aws configure

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

The aws configure command is used to set up the AWS CLI with your Access Key ID, Secret Access Key, default region, and output format so the CLI can authenticate and run commands against your AWS account.

Access keys are a pair of security credentials (Access Key ID and Secret Access Key) that allow programmatic access to AWS services through tools like the AWS CLI or SDKs, instead of logging in with a password.

The secret access key is like the password that pairs with your access key ID (your username). You need both to access AWS services.

### Best practice

The best practice alternative to using access keys is to use IAM roles (with temporary security credentials), especially with services like EC2, Lambda, or AWS SSO. This avoids hardcoding long-term credentials and improves security.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

Launch a bucket in Amazon S3.

### Step 5 - Connecting to my S3 bucket

Head back to your EC2 instance.
Get your EC2 instance to interact with your S3 bucket.


---

## Connecting to my S3 bucket

The first command I ran was aws s3 ls

When I ran the command aws s3 ls it showed the s3 bucket that i created.

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was aws s3 ls s3://kevinproject1 which returned the files uploaded inside the s3 bucket. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, sudo touch /tmp/test.txt, this creates an empty text file in my ec2. 

The second command I ran was aws s3 cp /tmp/test.txt s3://kevinproject1, this command copied/uploaded the empty file in the bucket kevinproject1. 

The third command I ran was aws s3 ls s3://kevinproject1, this command was used to check if the file was uploaded inside the s3 bucket. 

![Image](http://learn.nextwork.org/positive_azure_mysterious_prune/uploads/aws-networks-s3_3e1e79a2)

---

---
