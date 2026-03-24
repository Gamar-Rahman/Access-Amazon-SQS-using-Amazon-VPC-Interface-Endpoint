# Access-Amazon-SQS-using-Amazon-VPC-Interface-Endpoint
 Access Amazon SQS Using VPC Interface Endpoint (PrivateLink)
### Overview

This project demonstrates how to securely access Amazon SQS from within a VPC using an Interface Endpoint (AWS PrivateLink) — without exposing traffic to the public internet.

### Key Concepts

🔹 What is Amazon EC2?
EC2 provides scalable compute instances used to run applications inside a VPC.

🔹 What is Amazon VPC?
VPC is a logically isolated network where you control:
IP ranges
Subnets
Routing
Security

🔹 What is Amazon SQS?

Amazon SQS is a fully managed message queue service used to decouple applications.

### Problem Statement

By default, accessing AWS services like SQS may require:

Internet Gateway
NAT Gateway
Public endpoints

### This introduces:

Increased attack surface
Data exposure risks

Challenge:
How do we securely access SQS without using the public internet?

### Solution

We implemented:

VPC Interface Endpoint (PrivateLink) for SQS
Private communication between EC2 and SQS
No internet exposure

### Implementation Steps

🔹 Step 1: Create SQS Queue
Store and process messages

🔹 Step 2: Create VPC
Enable DNS hostnames
Configure subnets

🔹 Step 3: Configure Networking
Attach Internet Gateway (for setup/testing)
Update route tables

🔹 Step 4: Launch EC2 Instance
Configure security group
SSH into instance

🔹 Step 5: Create VPC Endpoint (SQS)
Select Interface endpoint
Attach security group
Enable private DNS

🔹 Step 6: Send Message to SQS

aws sqs send-message \
  --queue-url <QUEUE_URL> \
  --message-body "Hello from Private VPC"

### Security Controls Implemented  

✅ Private connectivity (no internet exposure)
✅ Reduced attack surface
✅ Security group enforcement
✅ AWS PrivateLink isolation

### Testing

| Test Case                 | Result     |
| ------------------------- | ---------- |
| Send message via endpoint | Success ✅  |
| Internet bypass attempt   | Blocked ❌  |
| Private DNS resolution    | Verified ✅ |


### Key Security Insight
Private connectivity is a core principle of cloud security.
Using VPC endpoints:
Eliminates dependency on public internet
Protects sensitive traffic
Strengthens Zero Trust architecture

### Future Improvements
Add endpoint policies
Integrate with IAM roles
Enable CloudTrail monitoring
Use private subnets only (no IGW)

