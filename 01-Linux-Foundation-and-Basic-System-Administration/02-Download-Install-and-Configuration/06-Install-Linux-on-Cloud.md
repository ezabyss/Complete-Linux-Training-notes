# Installing Linux on a Cloud Platform (AWS – Option 2)

How to install a Linux operating system on a cloud platform.
This is **Option 2** of the lab design.

If you are using **Option 1 (local VM using VMware or VirtualBox)**, you can safely skip this tutorial.

This guide is for learners who want to run Linux on a **cloud virtual machine**.

---

## How This Setup Works (Big Picture)

- You use your own computer (Windows or macOS)
- You open a web browser
- You access a cloud provider (AWS, Google Cloud, etc.)
- The cloud provider creates a virtual machine
- Linux is installed directly on that virtual machine

In cloud platforms, creating a virtual machine and installing Linux are usually **one combined step**.

---

## Cloud Platforms You Can Use

Common cloud platforms include:
- AWS (Amazon Web Services)
- Google Cloud Platform
- Azure

This tutorial demonstrates **AWS**, but the concept is similar across all cloud providers.

---

## Important Notes Before You Start

- You must create a **free cloud account**
- AWS Free Tier requires a **credit card**
- You will not be charged if you stay within free-tier limits
- If you do not have a credit card, use **Option 1 (local VM)** instead

---

## AWS Free Tier Limits (Very Important)

AWS Free Tier includes:
- 750 hours per month of a small virtual machine
- Up to 30 GB of storage

Rules to remember:
- One VM running full-time is safe
- Two VMs running together must still stay under 750 hours
- Storage above 30 GB will be charged
- AWS will not block you automatically — you must monitor usage

---

## Step 1: Create an AWS Free Account

1. Open your web browser
2. Search for: AWS free account
3. Click on: AWS Free Tier
4. Create an account using:
   - Email address
   - Account name
   - Credit card details

If you already have an AWS account, log in.

---

## Step 2: Access the EC2 Dashboard

After login:
- Open the AWS console
- Search for EC2 (Elastic Compute Cloud)
- Open the EC2 dashboard

EC2 is the service used to create virtual machines.

---

## Step 3: Choose a Region

- Select a region closest to your location
- Example:
  - US East (Ohio)
  - US East (N. Virginia)

Region choice does not affect free tier eligibility.

---

## Step 4: Launch a New Instance

1. Click on Launch Instance
2. Enter an instance name (example: my-linux-vm)

---

## Step 5: Choose an Operating System (AMI)

AMI means Amazon Machine Image.
It is a prebuilt virtual machine template.

Notes:
- CentOS may not appear directly
- Red Hat Enterprise Linux (RHEL) is equivalent in structure

Choose:
- Red Hat Enterprise Linux
- 64-bit architecture
- Leave default selection

---

## Step 6: Choose Instance Type

Select:
- t2.micro (Free Tier eligible)

This provides:
- 1 CPU
- 1 GB RAM

Leave default and continue.

---

## Step 7: Create or Select a Key Pair

A key pair is required to connect to the VM using SSH.

If new:
- Click Create new key pair
- Choose a name you will remember
- Download the key file
- Save it securely

This key is required later for SSH access (using tools like PuTTY).

---

## Step 8: Configure Network and Security

- Allow SSH traffic
- Source: Anywhere (for learning purposes)

This allows you to connect remotely to the VM.

---

## Step 9: Configure Storage

- Set storage between 10 GB and 30 GB
- Recommended: 20 GB
- Do NOT exceed 30 GB (or AWS will charge)

---

## Step 10: Launch the Instance

- Review settings
- Click Launch Instance

AWS will now:
- Create a virtual machine
- Install Linux automatically
- Start the system

---

## Step 11: Access the Linux VM

Once the instance is running:
- Use SSH to connect
- You can connect from:
  - Your local computer
  - Anywhere with internet access

This Linux system is now running in the cloud.

---

## Key Learning Notes

- Cloud VMs are real servers
- You do not install Linux manually like local VMs
- Cloud platforms bundle OS + VM creation
- Always stop the instance when not in use to avoid charges

---

## Final Reminder

If you want strict step-by-step consistency with the course:
- Use Option 1 (local VM)

If you want real-world server experience:
- Use Option 2 (cloud VM)

Both options are valid for learning Linux.

---

**✍️Notes By Abhishek (Ez Abyss)**
