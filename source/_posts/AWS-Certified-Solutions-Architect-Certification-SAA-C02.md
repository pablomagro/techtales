---
title: AWS Certified Solutions Architect Certification SAA-C02
date: 2020-05-13 22:55:28
tags:
  - Certifications
categories:
  - AWS
---

## AWS Account Activation Troubleshooting

Ensuring your AWS Account is activated (please read)


Before proceeding with the course, you need to make sure your account is activated

The activation email looks like this (the content might be slightly different for you):


Note: The text might be slightly different for you, but as long as AWS says thank you, or welcome, and tells you to start using your account, it should mean it's activated.

Example: A student received "Thank you for creating an Amazon Web Services (AWS) account. For the next 12 months, you will have free access to compute, storage, database, and application services. Learn more by visiting our Free Tier page. To access your account, click Access Account"

-----

To have your account activated, make sure to:

Add a Payment Method

Verify your phone number

Choose an AWS Support Plan (Free)

If your account is not activated yet, you will see this kind of error messages in the next lecture:

How to get an account activation email? (can take up to 24 hours, usually few minutes)

After you choose a Support plan, a confirmation page indicates that your account is being activated. Accounts are usually activated within a few minutes, but the process might take up to 24 hours.

You can sign in to your AWS account during this time. The AWS home page might display a button that shows "Complete Sign Up" during this time, even if you've completed all the steps in the sign-up process.

When your account is fully activated, you'll receive a confirmation email. After you receive this email, you have full access to all AWS services.

Troubleshooting delays in account activation

Account activation can sometimes be delayed. If the process takes more than 24 hours, check the following:

Finish the account activation process. You might have accidentally closed the window for the sign-up process before you've added all the necessary information. To finish the sign-up process, open https://aws-portal.amazon.com/gp/aws/developer/registration/index.html and sign in using the email address and password you chose for the account.

Check the information associated with your payment method. Check Payment Methods in the AWS Billing and Cost Management console. Fix any errors in the information.

Contact your financial institution. Financial institutions occasionally reject authorization requests from AWS for various reasons. Contact your payment method's issuing institution and ask that they approve authorization requests from AWS.
Note: AWS cancels the authorization request as soon as it's approved by your financial institution. You aren't charged for authorization requests from AWS. Authorization requests might still appear as a small charge (usually 1 USD) on statements from your financial institution.

Check your email for requests for additional information. Check your email to see if AWS needs any information from you to complete the activation process.

Try a different browser.

Contact AWS Support. Contact AWS Support for help. Be sure to mention any troubleshooting steps that you already tried.
Note: Don't provide sensitive information, such as credit card numbers, in any correspondence with AWS.

How to Contact AWS Support?

The top right corner will have Support > Support Center.

Ask them to activate the account, that can take up to 24 hours

Where to find more details?

Details can be found here: https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/


## Section 3: AWS Fundamentals: IAM & EC2

### 11. AWS Regions and AZs

- AWS has Regions all around the world.
- Names can be: us-east-1, eu-west-3…
- A region is a cluster of data centers.
- Most AWS services are region-scoped.

**AWS Availability Zones**
- Each region has many availability zones (usually 3, min is 2, max is 6). Example:
  - ap-southeast-2a
  - ap-southeast-2b
  - ap-southeast-2c
- Each availability zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity.
- They’re separate from each other, so that they’re isolated from disasters.
- They’re connected with high bandwidth, ultra-low latency networking.

  This helps guarantee that multi AZ won't all fail at once (due to a meteorological disaster for example). Read more here: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html

[https://aws.amazon.com/about-aws/global-infrastructure/](https://aws.amazon.com/about-aws/global-infrastructure/)

### IAM Introduction
- IAM (Identity and Access Management)
- Your whole AWS security is there:
  - Users
  - Groups
  - Roles
- Root account should never be used (and shared)
- Users must be created with proper permissions.
- IAM is at the center of AWS.
- Policies are written in JSON (JavaScript Object Notation.


- IAM has a global view.
- Permissions are governed by Policies (JSON).
- MFA (Multi Factor Authentication) can be setup. ***
- IAM has predefined “managed policies”.
- We’ll see IAM policies in details in the future.
- It’s best to give users the minimal amount of permissions they need to perform their job (least privilege principles).

  IAM is a global service (encompasses all regions)

  Q: You are getting started with AWS and your manager wants things to remain simple yet secure. He wants the management of engineers to be easy, and not re-invent the wheel every time someone joins your company. What will you do?
  A: I'll create multiple IAM users and groups, and assign policies to groups. New users will be added to groups


**IAM Federation**
- Big enterprises usually integrate their own repository of users with IAM
- This way, one can login into AWS using their company credentials
- Identity Federation uses the SAML standard (Active Directory)

**IAM 101 Brain Dump**
- One IAM User per PHYSICAL PERSON
- One IAM Role per Application
- IAM credentials should NEVER BE SHARED
- Never, ever, ever, ever, write IAM credentials in code. EVER.
- And even less, NEVER EVER EVER COMMIT YOUR IAM credentials
- Never use the ROOT account except for initial setup.
- Never use ROOT IAM Credentials

### What is EC2?
- EC2 is one of most popular of AWS offering
- It mainly consists in the capability of :
- Renting virtual machines (EC2)
- Storing data on virtual drives (EBS)
- Distributing load across machines (ELB)
- Scaling the services using an auto-scaling group (ASG)
- Knowing EC2 is fundamental to understand how the Cloud works


**Hands-On:**
Launching an EC2 Instance running Linux
- We’ll be launching our first virtual server using the AWS Console
- We’ll get a first high level approach to the various parameters
- We’ll learn how to start / stop / terminate our instance.


**Add Tags**
Define pairs, to identify the instances.

**Security Group**
Define the firewall around the instances

## How to SSH into your EC2 Instance
Linux / Mac OS X
- We’ll learn how to SSH into your EC2 instance using Linux / Mac.
- SSH is one of the most important function. It allows you to control a remote machine, all using the command line.
- We will see how we can configure OpenSSH ~/.ssh/config to facilitate the SSH into our EC2 instances.

Public DNS (IPv4)
ec2-54-153-150-4.ap-southeast-2.compute.amazonaws.com
IPv4 Public IP 54.153.150.4

ssh ec2-user@ec2-54-153-150-4.ap-southeast-2.compute.amazonaws.com
ssh ec2-user@54.153.150.4
ssh -i EC2Tutorial.pem ec2-user@54.153.150.4

  Q: You are getting a permission error exception when trying to SSH into your Linux Instance
  A: the key is missing permissions chmod 0400
  The exam expects you to know this, even if you used Windows / Putty to SSH into your instances. If you're a windows user, just have a quick look at the Linux SSH lecture!

## EC2 Instance Connect
- Connect to your EC2 instance within your browser
- No need to use your key file that was downloaded
- The “magic” is that a temporary key is uploaded onto EC2 by AWS
- Works only out-of-the-box with Amazon Linux 2
- Need to make sure the port 22 is still opened!

* EC2 Instance Connect (browser-based SSH connection): Connect to your instance using SSH in the console

## Introduction to Security Groups
- Security Groups are the fundamental of network security in AWS
- They control how traffic is allowed into or out of our EC2 Machines.
- It is the most fundamental skill to learn to troubleshoot networking issues.
- In this lecture, we’ll learn how to use them to allow, inbound and outbound ports.

**Security Groups Deeper Dive**

- ``Security groups are acting as a “firewall” on EC2 instances``.
- They regulate:
  - Access to Ports
  - Authorised IP ranges – IPv4 and IPv6
  - Control of inbound network (from other to the instance)
  - Control of outbound network (from the instance to other)

**Good to know**
- Can be attached to multiple instances
- Locked down to a region / VPC combination
- Does live “outside” the EC2 – if traffic is blocked the EC2 instance won’t see it
- ``It’s good to maintain one separate security group for SSH access``
- If your application is not accessible (time out), then it’s a security group issue
- If your application gives a “connection refused“ error, then it’s an application error or it’s not launched
- All inbound traffic is ``blocked`` by default
- All outbound traffic is ``authorised`` by default

  Q: Security groups can reference all of the following except:
      - IP Address
      - CIDR block
      - Security Group
      - DNS name        [ok]

## Private vs Public IP (IPv4)
- Networking has two sorts of IPs. IPv4 and IPv6:
- IPv4: 1.160.10.240
- IPv6: 3ffe:1900:4545:3:200:f8ff:fe21:67cf
- In this course, we will only be using IPv4.
- IPv4 is still the most common format used online.
- IPv6 is newer and solves problems for the Internet of Things (IoT).
- IPv4 allows for ``3.7 billion`` different addresses in the public space
- IPv4: [0-255].[0-255].[0-255].[0-255].


**Fundamental Differences**
- Public IP:
  - Public IP means the machine can be identified on the internet (WWW)
  - Must be unique across the whole web (not two machines can have the same public IP).
  - Can be geo-located easily
- Private IP:
  - Private IP means the machine can only be identified on a private network only
  - The IP must be unique across the private network
  - BUT two different private networks (two companies) can have the same IPs.
  - Machines connect to WWW using a NAT + internet gateway (a proxy)
  - Only a specified range of IPs can be used as private IP


## Elastic IP
- With an Elastic IP address, you can mask the failure of an instance or software
by rapidly remapping the address to another instance in your account.

- You can only have 5 Elastic IP in your account (you can ask AWS to increase
that).

- Overall, ``try to avoid using Elastic IP``:
  - They often reflect poor architectural decisions
  - Instead, use a random public IP and register a DNS name to it
  - Or, as we’ll see later,`` use a Load Balancer and don’t use a public IP`` best pattern (*)


## Private vs Public IP (IPv4)
AWS EC2 – Hands On
- By default, your EC2 machine comes with:
  - A private IP for the internal AWS Network
  - A public IP, for the WWW.

- When we are doing SSH into our EC2 machines:
  - We can’t use a private IP, because we are not in the same network
  - We can only use the public IP.
- If your machine is stopped and then started, ``the public IP can change``

**Launching an Apache Server on EC2**
- Let’s leverage our EC2 instance
- We’ll install an Apache Web Server to display a web page
- We’ll create an index.html that shows the hostname of our machine


```bash
yum install -y httpd.x86_64

systemctl start httpd.service

# Enable across reboot .
systemctl enable httpd.service

# First test page
echo "Hello World from $(hostname -f)" > /var/www/html/index.html
```


**EC2 User Data**
- It is possible to bootstrap our instances using an ``EC2 User data`` script.
- ``bootstrapping`` means launching commands when a machine starts.
- That script is ``only run once`` at the instance ``first start``
- EC2 user data is used to automate boot tasks such as:
  - Installing updates
  - Installing software
  - Downloading common files from the internet
  - Anything you can think of
- The EC2 User Data Script runs with the root user.

**More EC2 User Data**
Hands-On
- We want to make sure that this EC2 instance has an Apache HTTP
server installed on it – to display a simple web page
- For it, we are going to write a user-data script.
- This script will be executed at the first boot of the instance.
- Let’s get hands on!

1) Terminate instance.
2) Create instances
  - Linux 2
  - Step 3:
    User data, ``As text``
    ```bash
    #!/bin/bash
    # Use this for your user data (script without newlines)
    # install httpd (Linux 2 version)
    yum update -y
    yum install -y httpd.x86_64
    systemctl start httpd.service
    systemctl enable httpd.service
    echo "Hello World from $(hostname -f)" > /var/www/html/index.html
    ```

**EC2 Instance Launch Types**
- On Demand Instances: short workload, predictable pricing.
- Reserved: (MINIMUM 1 year) E.g: A database.
  - Reserved Instances: long workloads
  - Convertible Reserved Instances: long workloads with flexible instances.
  - Scheduled Reserved Instances: example – every Thursday between 3 and 6 pm
- Spot Instances: short workloads, for cheap, can lose instances (``less reliable``)
- Dedicated Instances: no other customers will share your hardware.
- Dedicated Hosts: book an entire physical server, control instance placement.

**EC2 On Demand**
- Pay for what you use (billing per second, after the first minute).
- Has the highest cost but no upfront payment
- No long term commitment

- Recommended for short-term and un-interrupted workloads, where you can't predict how the application will behave. Ideal for elastic workflows

**EC2 Reserved Instances**
- Up to 75% discount compared to On-demand
- Pay upfront for what you use with long term commitment
- Reservation period can be 1 or 3 years
- Reserve a specific instance type
- Recommended for steady state usage applications (think ```database```)

- Convertible Reserved Instance
  - Can change the EC2 instance type (you can make it evolve).
  - Up to 54% discount.
- Scheduled Reserved Instances
  - launch within time window you reserve
  - When you require a fraction of day / week / month

**EC2 Spot Instances**
- Can get a discount of up to 90% compared to On-demand
- Instances that you can “lose” at any point of time if your max price is less than the current spot price
- The MOST cost-efficient instances in AWS
- **Useful for workloads that are resilient to failure**
  - Batch jobs
  - Data analysis
  - Image processing
  - …
- **Not great for critical jobs or databases**

- **Great combo: Reserved Instances for baseline (Web app) + On-Demand & Spot for peaks (Unpredictable, more agility, save money)**

Q: You plan on running an open-source MongoDB database year-round on EC2. Which instance launch mode should you choose?
A: Reserved instances
    This will allow you to save cost as you know in advance that the instance will be a up for a full year


**EC2 Dedicated Hosts**
- Physical dedicated EC2 server for your use
- Full control of EC2 Instance placement
- Visibility into the underlying sockets / physical cores of the hardware
- Allocated for your account for a ``3 year period`` reservation
- ``More expensive``

- Useful for software that have complicated licensing model (BYOL – Bring Your Own License)
- Or for companies that have strong regulatory or compliance needs.

**EC2 Dedicated Instances**
- Instances running on hardware that’s dedicated to you.
- May share hardware with other instances in same account.
- No control over instance placement (can move hardware after Stop / Start).

**Which host is right for me?**
- On demand: coming and staying in resort whenever we like, we pay the full price
- Reserved: like planning ahead and if we plan to stay for a long time, we may get a good discount.
- Spot instances: the hotel allows people to bid for the empty rooms and the highest bidder
keeps the rooms. You can get kicked out at any time
- Dedicated Hosts: We book an entire building of the resort


Q: You would like to deploy a database technology and the vendor license bills you based on the physical cores and underlying network socket visibility. Which EC2 launch modes allow you to get visibility into them?
A: Dedicated Hosts.


**Price Comparison**
Example – m4.large – us-east-1
Price Type Price (per hour)
On-demand $0.10
Spot Instance (Spot Price) $0.032 - $0.045 (up to 90% off)
Spot Block (1 to 6 hours) ~ Spot Price
Reserved Instance (12 months) – no upfront $0.062
Reserved Instance (12 months) – all upfront $0.058
Reserved Instance (36 months) – no upfront $0.043
Reserved Convertible Instance (12 months) – no upfront $0.071
Reserved Dedicated Instance (12 months) – all upfront $0.064
Reserved Scheduled Instance (recurring schedule on 12 months term) $0.090 – $0.095 (5%-10% off)
Dedicated Host On-demand price
Dedicated Host Reservation Up to 70% off

**EC2 Spot Instance Requests**
- Can get a discount of up to 90% compared to On-demand

- Define *max spot price* and get the instance while **current spot price < max**
  - The hourly spot price varies based on offer and capacity
  - If the current spot price > your max price you can choose to **stop** or **terminate** your instance with a 2 minutes grace period.
- Other strategy: **Spot Block**
  - “block” spot instance during a specified time frame (1 to 6 hours) without interruptions
  - In rare situations, *the instance may be reclaimed*

- **Used for batch jobs, data analysis, or workloads that are resilient to failures**.
- **Not great for critical jobs or databases**

*EC2 Spot Instances Pricing*
https://console.aws.amazon.com/

**Spot Fleets**
- Spot Fleets = set of Spot Instances + (optional) On-Demand Instances
- The Spot Fleet will try to meet the target capacity with price constraints
  - Define possible **launch pools**: instance type (m5.large), OS, Availability Zone
  - Can have multiple launch pools, so that the fleet can choose
  - Spot Fleet stops launching instances when reaching capacity or max cost
- Strategies to allocate Spot Instances:
  - **lowestPrice**: from the pool with the lowest price (cost optimization, short workload)
  - **diversified**: distributed across all pools (great for availability, long workloads)
  - **capacityOptimized**: pool with the optimal capacity for the number of instances

- __Spot Fleets allow us to automatically request Spot Instances with the lowest price__

**EC2 Instance Types – Main ones**
- R: applications that needs a lot of RAM – in-memory caches
- C: applications that needs good CPU – compute / databases
- M: applications that are balanced (think “medium”) – general / web app
- I: applications that need good local I/O (instance storage) – databases
- G: applications that need a GPU – video rendering / machine learning

- T2 / T3: burstable instances (up to a capacity)
- T2 / T3 - unlimited: unlimited burst

- Real-world tip: use https://www.ec2instances.info

**Burstable Instances (T2/T3)**
- AWS has the concept of burstable instances (T2/T3 machines).

- Burst means that overall, the instance has OK CPU performance.
- When the machine needs to process something unexpected (a spike in
load for example), it can burst, and CPU can be VERY good.
- If the machine bursts, it utilizes “**burst credits**”
- If all the credits are gone, the CPU becomes BAD
- If the machine stops bursting, credits are accumulated over time

- Burstable instances can be amazing to handle unexpected traffic and getting the insurance that it will be handled correctly
- If your instance consistently runs low on credit, you need to move to a different kind of non-burstable instance Credit usage Credit balance

**T2/T3 Unlimited**
- Nov 2017: It is possible to have an “unlimited burst credit balance”
- You pay extra money if you go over your credit balance, but you don’t
lose in performance

- Overall, it is a new offering, so be careful, costs could go high if you’re
not monitoring the health of your instances

- Read more here: https://aws.amazon.com/blogs/aws/new-t2-unlimitedgoing-beyond-the-burst-with-high-performance


## What’s an AMI?
- As we saw, AWS comes with base images such as:
  - Ubuntu
  - Fedora
  - RedHat
  - Windows
  - Etc…
- These images can be customised at runtime using EC2 User data

- But what if we could create our own image, ready to go?
- That’s an AMI – **an image to use to create our instances**
- AMIs can be built for Linux or Windows machines

**Why would you use a custom AMI?**
- Using a custom built AMI can provide the following advantages:
  - Pre-installed packages needed
  - Faster boot time (no need for ec2 user data at boot time)
  - Machine comes configured with monitoring / enterprise software
  - Security concerns – control over the machines in the network
  - Control of maintenance and updates of AMIs over time
  - Active Directory Integration out of the box
  - Installing your app ahead of time (for faster deploys when auto-scaling)
  - Using someone else’s AMI that is optimised for running an app, DB, etc…
- AMI are built for a specific AWS region (!) **NO GLOBAL**

Q: You built and published an AMI in the ap-southeast-2 region, and your colleague in us-east-1 region cannot see it
A: An AMI created for a region can only be seen in that region.

Q: You are launching an EC2 instance in us-east-1 using this Python script snippet:

(we will see SDK in a later section, for now just look at the code reference ImageId)

ec2.create_instances(ImageId='ami-b23a5e7', MinCount=1, MaxCount=1)
It works well, so you decide to deploy your script in us-west-1 as well. There, the script does not work and fails with "ami not found" error. What's the problem?
A: AMI is region locked and the same ID cannot be used across regions

**Using Public AMIs**
- You can leverage AMIs from other people
- You can also pay for other people’s AMI by the hour
  - These people have optimised the software
  - The machine is easy to run and configure
  - You basically rent “expertise” from the AMI creator

- AMI can be found and published on the Amazon Marketplace

- **Warning**:
  - Do not use an AMI you don’t trust!
  - Some AMIs might come with malware or may not be secure for your enterprise

**AMI Storage**
- Your AMI take space and they live in Amazon S3

- Amazon S3 is a durable, cheap and resilient storage where most of your
backups will live (but you won’t see them in the S3 console)

- By default, your AMIs are private, and locked for your account / region

- You can also make your AMIs public and share them with other AWS
accounts or sell them on the AMI Marketplace

**AMI Pricing**
- AMIs live in Amazon S3, so you get charged for the actual space in takes in Amazon S3

- Amazon S3 pricing in US-EAST-1:
  - First 50 TB / month: $0.023 per GB
  - Next 450 TB / month: $0.022 per GB

- Overall it is quite inexpensive to store private AMIs.
- Make sure to remove the AMIs you don’t use





**Cross Account AMI Copy (FAQ + Exam Tip)**
- You can share an AMI with another AWS account.
- Sharing an AMI does not affect the ownership of the AMI.
- **If you copy an AMI that has been shared with your account, you are the owner of the target AMI in your account**.
- To copy an AMI that was shared with you from another account, the owner of the source AMI must grant you read permissions for the storage that backs the AMI, either the associated EBS snapshot (for an Amazon EBS-backed AMI) or an associated S3 bucket (for an instance store-backed AMI).
- **Limits**:
- You can't copy an encrypted AMI that was shared with you from another account. Instead, **if the underlying snapshot and encryption key were shared with you, you can copy the snapshot while re-encrypting it with a key of your own. You own the copied snapshot, and can register it as a new AMI.** [*]
- You can't copy an AMI with an associated **billingProduct** code that was shared with you from another account. This includes Windows AMIs and AMIs from the AWS Marketplace. To copy a shared AMI with a **billingProduct** code, **launch an EC2 instance in your account using the shared AMI and then create an AMI from the instance**. [*]

[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Copy](https://docs.aws.amazon.ingAMIs.html)

## Placement Groups
- Sometimes you want control over the EC2 Instance placement strategy
- That strategy can be defined using placement groups
- When you create a placement group, you specify one of the following
strategies for the group:
  - Cluster—clusters instances into a low-latency group in a single Availability Zone
  - Spread—spreads instances across underlying hardware (max 7 instances per
  group per AZ) - critical applications
  - Partition—spreads instances across many different partitions (which rely on
  different sets of racks) within an AZ. Scales to 100s of EC2 instances per group
  (Hadoop, Cassandra, Kafka)

### Cluster
- Pros: Great network (10 Gbps bandwidth between instances)
- Cons: If the rack fails, all instances fails at the same time
- Use case:
  - Big Data job that needs to complete fast
  - Application that needs extremely low latency and high network throughput

### Spread
- Pros:
  - Can span across Availability Zones (AZ)
  - Reduced risk is simultaneous failure
  - **EC2** Instances are on **different physical hardware**
- Cons:
  - Limited to **7 instances per AZ per placement group** [*]
- Use case:
  - Application that needs to maximize high availability
  - Critical Applications where each instance must be isolated from failure from each other EC2

### Partition
- Up to 7 partitions per AZ
- Up to 100s of EC2 instances
- The instances in a partition do not share racks with the instances in the other partitions
- A partition failure can affect many EC2 but won’t affect other partitions
- EC2 instances get access to the partition information as metadata
- Use cases: HDFS, HBase, Cassandra, Kafka

Q: You would like to make sure your EC2 instances have the highest performance while talking to each other as you're performing big data analysis. Which placement group should you choose?
A: Cluster
    Cluster placement groups places your instances next to each other giving you high performance computing and networking

Q: You are launching an application on EC2 and the whole process of installing the application takes about 30 minutes. You would like to minimize the total time for your instance to boot up and be operational to serve traffic. What do you recommend?
A: Create an AMI after installing and launch from the AMI
    Creating an AMI after installing the applications allows you to start more EC2 instances directly from that AMI, hence bypassing the need to install the application (as it's already installed)

Q: You are running a critical workload of three hours per week, on Monday. As a solutions architect, which EC2 Instance Launch Type should you choose to maximize the cost savings while ensuring the application stability?
A: Scheduled Reserved Instances

## Elastic Network Interfaces (ENI)
- Logical component in a VPC that represent **a virtual network card**
- The ENI can have the following attributes:
  - Primary private IPv4, one or more secondary IPv4
  - One Elastic IP (IPv4) per private IPv4
  - One Public IPv4
  - One or more security groups
  - A MAC address
- You can create ENI independently and attach them on the fly (move them) on EC2 instances for failover
- Bound to a specific availability zone (AZ)

## EC2 Hibernate
- We know we can stop, terminate instances
  - Stop: the data on disk (EBS) is kept intact in the next start
  - Terminate: any EBS volumes (root) also set-up to be destroyed is lost

- On start, the following happens:
  - First start: the OS boots & the EC2 User Data script is run
  - Following starts: the OS boots up
  - Then your application starts, caches get warmed up, and that can take time!

**EC2 Hibernate**
- Introducing **EC2 Hibernate**:
  - **The in-memory (RAM) state is preserved**
  - The instance boot is much faster! (the OS is not stopped / restarted)
  - Under the hood: the RAM state is written to a file in the root EBS volume
  - The root EBS **volume must be encrypted**

- **Use cases:**
  - long-running processing
  - saving the RAM state
  - services that take time to initialize
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Hibernate.html

**EC2 Hibernate – Good to know**
- **Supported instance families** - C3, C4, C5, M3, M4, M5, R3, R4, and R5.
- **Instance RAM size** - must be less than 150 GB.
- **Instance size** - not supported for bare metal instances.
- **AMI**: Amazon Linux 2, Linux AMI, Ubuntu & Windows…
- **Root Volume**: must be EBS, encrypted, not instance store, and large
- Available for On-Demand and Reserved Instances

- An instance cannot be hibernated more than 60 days

## EC2 for Solutions Architects
- EC2 instances are billed by the second, t2.micro is free tier
- On Linux / Mac we use SSH, on Windows we use Putty
- SSH is on port 22, lock down the security group to your IP
- Timeout issues => Security groups issues
- Permission issues on the SSH key => run “chmod 0400”
- Security Groups can reference other Security Groups instead of IP
ranges (very popular exam question)
- Know the difference between Private, Public and Elastic IP
- You can customize an EC2 instance at boot time using EC2 User Data

**EC2 for Solutions Architects**
- Know the 4 EC2 launch modes:
  - On demand
  - Reserved
  - Spot instances
  - Dedicated Hosts
- Know the basic instance types: R,C,M,I,G, T2/T3
- You can create AMIs to pre-install software on your EC2 => faster boot
- AMI can be copied across regions and accounts
- EC2 instances can be started in placement groups:
  - Cluster
  - Spread


# Section 4: High Availability and Scalability: ELB & ASG


## Scalability & High Availability ##
- Scalability means that an application / system can handle greater loads by adapting.
- There are two kinds of scalability:
  - Vertical Scalability
  - Horizontal Scalability (= elasticity)
- **Scalability is linked but different to High Availability**
- Let’s deep dive into the distinction, using a call center as an example

**Vertical Scalability**
- Vertically scalability means **increasing the size of the instance**
- For example, your application runs on a t2.micro
- Scaling that application vertically means running it on a t2.large
- Vertical scalability is very common for non distributed systems, such as a database.
- RDS, ElastiCache are services that can scale vertically.
- There’s usually a limit to how much you can vertically scale (hardware limit) junior operator senior operator

**Horizontal Scalability**
- Horizontal Scalability means **increasing the number of instances / systems for your application**

- Horizontal scaling implies distributed systems.
- This is very common for web applications / modern applications

- It’s easy to horizontally scale thanks the cloud offerings such as Amazon EC2

## High Availability first building in New York
- High Availability usually goes hand in hand with horizontal scaling
- High availability means running your application / system in at least 2 data
centers (== Availability Zones)
- The goal of high availability is to survive a data center loss

- The high availability can be passive (for RDS Multi AZ for example)
- The high availability can be active (for horizontal scaling)

## High Availability & Scalability For EC2
- Vertical Scaling: **Increase instance size** (= scale up / down)
  - From: t2.nano - 0.5G of RAM, 1 vCPU
  - To: u-12tb1.metal – 12.3 TB of RAM, 448 vCPUs

- Horizontal Scaling: **Increase number of instances** (= scale out / in)
  - Auto Scaling Group
  - Load Balancer

- High Availability: Run instances for the same application across multi AZ
  - Auto Scaling Group multi AZ
  - Load Balancer multi AZ

## What is load balancing?
- Load balancers are servers that **forward internet traffic to multiple servers (EC2 Instances)** downstream.

## Why use a load balancer?
- Spread load across multiple downstream instances
- **Expose a single point of access (DNS) to your application**
- Seamlessly handle failures of downstream instances
- Do regular health checks to your instances
- Provide SSL termination (HTTPS) for your websites
- Enforce stickiness with cookies
- High availability across zones - Separate public traffic from private traffic

## Why use an EC2 Load Balancer?
- An ELB (EC2 Load Balancer) is a **managed load balancer**
  - AWS guarantees that it will be working
  - AWS takes care of upgrades, maintenance, high availability
  - AWS provides only a few configuration knobs

- It costs less to setup your own load balancer but it will be a lot more effort on your end.

- It is integrated with many AWS offerings / services

**Health Checks**
- Health Checks are crucial for Load Balancers
- They enable the load balancer to know if instances it forwards traffic to are available to reply to requests
- The health check is done on a port and a route (/health is common)
- **(If the response is not 200 (OK), then the instance is unhealthy)**

**Types of load balancer on AWS**
- AWS has **3 kinds of managed Load Balancers**

- Classic Load Balancer (v1 - old generation) – 2009
  - HTTP, HTTPS, TCP
- Application Load Balancer (v2 - new generation) – 2016
  - HTTP, HTTPS, WebSocket
- Network Load Balancer (v2 - new generation) – 2017
  - TCP, TLS (secure TCP) & UDP
- Overall, it is recommended to use the newer / v2 generation load balancers as they
provide more features

- You can setup **internal** (private) or **external** (public) ELBs

**Load Balancer**
**Good to Know**
- LBs can scale but not instantaneously – contact AWS for a “warm-up”
- Troubleshooting
  - 4xx errors are client induced errors
  - 5xx errors are application induced errors
  - Load Balancer Errors 503 means at capacity or no registered target
  - If the LB can’t connect to your application, check your security groups!
- Monitoring
  - ELB access logs will log all access requests (so you can debug per request)
  - CloudWatch Metrics will give you aggregate statistics (ex: connections count)

### Classic Load Balancers (v1)
- Supports **TCP** (Layer 4), **HTTP** & **HTTPS** (Layer 7)
- Health checks are TCP or HTTP based
- Fixed hostname XXX.region.elb.amazonaws.com

### Application Load Balancer (v2)
- Application load balancers is Layer 7 (HTTP)

- Load balancing to multiple HTTP applications across machines (**target groups**)
- Load balancing to multiple applications on the same machine (ex: containers)
- Support for HTTP/2 and WebSocket
- Support redirects (from HTTP to HTTPS for example)

- Routing tables to different target groups:
  - Routing based on path in URL (example.com/users & example.com/posts)
  - Routing based on hostname in URL (one.example.com & other.example.com)
  - Routing based on Query String, Headers (example.com/users?id=123&order=false)

- **ALB are a great fit for micro services & container-based application** (example: Docker & Amazon ECS)
- Has a port mapping feature to redirect to a dynamic port in ECS
- In comparison, we’d need multiple Classic Load Balancer per application

**Application Load Balancer (v2)**
**Target Groups**
- EC2 instances (can be managed by an Auto Scaling Group) – HTTP
- ECS tasks (managed by ECS itself) – HTTP
- Lambda functions – HTTP request is translated into a JSON event
- IP Addresses – must be private IPs

- ALB can route to multiple target groups
- Health checks are at the target group level

### Good to Know
- Fixed hostname (XXX.region.elb.amazonaws.com)
- The application servers don’t see the IP of the client directly
  - The true IP of the client is inserted in the header **X-Forwarded-For**
  - We can also get Port (**X-Forwarded-Port**) and proto (**X-Forwarded-Proto**)

## Network Load Balancer (v2)
- Network load balancers (Layer 4) allow to:
  - **Forward TCP & UDP traffic to your instances**
  - Handle millions of request per seconds
  - Less latency ~100 ms (vs 400 ms for ALB)

- **NLB has one static IP per AZ, and supports assigning Elastic IP** (helpful for whitelisting specific IP)

- NLB are used for extreme performance, TCP or UDP traffic
- Not included in the AWS free tier

## Load Balancer Stickiness
- It is possible to implement stickiness so that the same client is always redirected
to the same instance behind a load balancer
- This works for Classic Load Balancers & Application Load Balancers
- The “cookie” used for stickiness has an expiration date you control
- Use case: make sure the user doesn’t lose his session data
- Enabling stickiness may bring imbalance to the load over the backend EC2 instances

## Cross-Zone Load Balancing
- It is possible to implement stickiness so that the same client is always redirected
to the same instance behind a load balancer
- This works for Classic Load Balancers & Application Load Balancers
- The “cookie” used for stickiness has an expiration date you control
- Use case: make sure the user doesn’t lose his session data
- Enabling stickiness may bring imbalance to the load over the backend EC2 instances

- **With Cross Zone Load Balancing: each load balancer instance distributes evenly across all registered instances in all AZ**
- Otherwise, each load balancer node distributes requests evenly across the registered instances in its Availability Zone only

- Classic Load Balancer
  - **Disabled by default**
  - No charges for inter AZ data if enabled

- Application Load Balancer
  - Always on (can’t be disabled)
  - No charges for inter AZ data

- Network Load Balancer
  - Disabled by default
  - **You pay charges** ($) for inter AZ data if enabled

## SSL/TLS - Basics
- An SSL Certificate allows traffic between your clients and your load balancer
to be encrypted in transit (in-flight encryption)

- SSL refers to Secure Sockets Layer, used to encrypt connections
- TLS refers to Transport Layer Security, which is a newer version
- Nowadays, **TLS certificates are mainly used**, but people still refer as SSL

- Public SSL certificates are issued by Certificate Authorities (CA)
- Comodo, Symantec, GoDaddy, GlobalSign, Digicert, Letsencrypt, etc…

- SSL certificates have an expiration date (you set) and must be renewed

## Load Balancer - SSL Certificates
- The load balancer uses an **X.509 certificate (SSL/TLS server certificate)**
- You can manage certificates using ACM (AWS Certificate Manager)
- You can create upload your own certificates alternatively
- HTTPS listener:
  - You must specify a default certificate
  - You can add an optional list of certs to support multiple domains
  - **Clients can use SNI (Server Name Indication) to specify the hostname they reach**
  - Ability to specify a security policy to support older versions of SSL / TLS (legacy clients)

## SSL – Server Name Indication (SNI)
- SNI solves the problem of loading **multiple SSL certificates onto one web server** (to serve multiple websites)
- It’s a “newer” protocol, and requires the client to **indicate** the hostname of the target server in the initial SSL handshake
- The server will then find the correct certificate, or return the default one

**Note:**
- Only works for ALB & NLB (newer generation), CloudFront
- Does not work for CLB (older gen)

## Elastic Load Balancers – SSL Certificates
- **Classic Load Balancer (v1)**
  - Support only one SSL certificate
  - Must use multiple CLB for multiple hostname with multiple SSL certificates

- **Application Load Balancer (v2)**
  - Supports multiple listeners with multiple SSL certificates
  - Uses Server Name Indication (SNI) to make it work

- **Network Load Balancer (v2)**
  - Supports multiple listeners with multiple SSL certificates
  - Uses Server Name Indication (SNI) to make it work

## ELB – Connection Draining [*]
- **Feature naming**:
  - CLB: Connection Draining
  - Target Group: Deregistration Delay (for ALB & NLB)

- **Time to complete “in-flight requests” while the instance is de-registering or unhealthy**
- Stops sending new requests to the instance which is de-registering
- Between 1 to 3600 seconds, default is 300 seconds
- Can be disabled (set value to 0)
- Set to a low value if your requests are short

## What’s an Auto Scaling Group?
In real-life, the load on your websites and application can change
- In the cloud, you can create and get rid of servers very quickly

- The goal of an Auto Scaling Group (ASG) is to:
  - Scale out (add EC2 instances) to match an increased load
  - Scale in (remove EC2 instances) to match a decreased load
  - Ensure we have a minimum and a maximum number of machines running
  - Automatically Register new instances

## ASGs have the following attributes
- A launch configuration
  - AMI + Instance Type
  - EC2 User Data
  - EBS Volumes
  - Security Groups
  - SSH Key Pair
- Min Size / Max Size / Initial Capacity
- Network + Subnets Information
- Load Balancer Information
- Scaling Policies

## Auto Scaling Alarms
- It is possible to scale an ASG based on CloudWatch alarms
- An Alarm monitors a metric (such as Average CPU)
- __Metrics are computed for the overall ASG instances__
- Based on the alarm:
  - We can create scale-out policies (increase the number of instances)
  - We can create scale-in policies (decrease the number of instances)

## Auto Scaling New Rules
- It is now possible to define ”better” auto scaling rules that are directly
managed by EC2
  - Target Average CPU Usage
  - Number of requests on the ELB per instance
  - Average Network In
  - Average Network Out
- These rules are easier to set up and can make more sense

## Auto Scaling Custom Metric
- We can auto scale based on a custom metric (ex: number of connected
users)

- 1. Send custom metric from application on EC2 to CloudWatch
(PutMetric API)
- 2. Create CloudWatch alarm to react to low / high values
- 3. Use the CloudWatch alarm as the scaling policy for ASG

## ASG Brain Dump
- Scaling policies can be on CPU, Network… and can even be on custom metrics or
based on a schedule (if you know your visitors patterns)
- ASGs use Launch configurations or Launch Templates (newer)
- To update an ASG, you must provide a new launch configuration / launch template
- IAM roles attached to an ASG will get assigned to EC2 instances
- ASG are free. You pay for the underlying resources being launched
- Having instances under an ASG means that if they get terminated for whatever reason, the ASG will automatically ***create new ones as a replacement***. Extra safety!
- ASG can terminate instances marked as unhealthy by an LB (and hence replace them)

## Auto Scaling Groups – Scaling Policies
- **Target Tracking Scaling**
  - Most simple and easy to set-up
  - Example: I want the average ASG CPU to stay at around 40%
- **Simple / Step Scaling**
  - When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 units
  - When a CloudWatch alarm is triggered (example CPU < 30%), then remove 1
- **Scheduled Actions**
  - Anticipate a scaling based on known usage patterns
  - Example: increase the min capacity to 10 at 5 pm on Fridays

## Auto Scaling Groups - Scaling Cooldowns
- **The cooldown period helps to ensure that your Auto Scaling group doesn't launch or terminate additional instances before the previous scaling activity takes effect**.
- In addition to default cooldown for Auto Scaling group, we can create cooldowns
that apply to a specific **simple scaling policy**
- A scaling-specific cooldown period overrides the default cooldown period.
- One common use for scaling-specific cooldowns is with a scale-in policy—a policy that terminates instances based on a specific criteria or metric. Because this policy
terminates instances, Amazon EC2 Auto Scaling needs less time to determine
whether to terminate additional instances.
- **If the default cooldown period of 300 seconds is too long—you can reduce costs y applying a scaling-specific cooldown period of 180 seconds to the scale-in policy**.
- If your application is scaling up and down multiple times each hour, modify the
Auto Scaling Groups cool-down timers and the CloudWatch Alarm Period that
triggers the scale in

## ASG for Solutions Architects
- **ASG Default Termination Policy (simplified version)**:
1. Find the AZ which has the most number of instances
2. If there are multiple instances in the AZ to choose from, delete the one with the oldest launch configuration
- ASG tries the balance the number of instances across AZ by default

**Lifecycle Hooks**
- By default as soon as an instance is launched in an ASG it’s in service.
- You have the ability to perform extra steps before the instance goes in service (Pending state)
- You have the ability to perform some actions before the instance is terminated(Terminating state)
https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-hooks.html

**Launch Template vs Launch Configuration**
- **Both**:
  - ID of the Amazon Machine Image (AMI), the instance type, a key pair, security  roups, and the other parameters that you use to launch EC2 instances (tags, EC2 user-data...)

- **Launch Configuration (legacy):**
  - Must be re-created every time

- **Launch Template (newer):**
  - Can have multiple versions
  - Create parameters subsets (partial configuration for re-use and inheritance)
  - Provision using both On-Demand and Spot instances (or a mix)
  - Can use T2 unlimited burst feature
  - __Recommended by AWS going forward__



  --------------------------

Q1: Load Balancers provide a
A: static DNS name we can use our application
  The reason being that AWS wants your load balancer to be accessible using a static endpoint, even if the underlying infrastructure that AWS manages changes

Q2: You are running a website with a load balancer and 10 EC2 instances. Your users are complaining about the fact that your website always asks them to re-authenticate when they switch pages. You are puzzled, because it's working just fine on your machine and in the dev environment with 1 server. What could be the reason?
A: The Load Balancer does not have stickiness enabled

  Stickiness ensures traffic is sent to the same backend instance for a client. This helps maintaining session data

Question 3:
Your application is using an Application Load Balancer. It turns out your application only sees traffic coming from private IP which are in fact your load balancer's. What should you do to find the true IP of the clients connected to your website?
A: Look into the X-Forwarded-For header in the backend

  This header is created by your load balancer and passed on to your backend application

Question 4:
A: Question 4:
You quickly created an ELB and it turns out your users are complaining about the fact that sometimes, the servers just don't work. You realise that indeed, your servers do crash from time to time. How to protect your users from seeing these crashes?
A: Enable Health Checks

  Health checks ensure your ELB won't send traffic to unhealthy (crashed) instances

Question 5:
You are designing a high performance application that will require millions of connections to be handled, as well as low latency. The best Load Balancer for this is
A: Network Load Balancer
  NLB provide the highest performance if your application needs it

Question 6:
Application Load Balancers handle all these protocols except
A: TCP
  Use a NLB (Network Load Balancer) support TCP instead

Question 7: X
The application load balancer can route to different target groups based on all these except...
A: Geography -  This was discussed in Lecture 40: Elastic Load Balancing (ELB) Overview
    X: Source IP

Question 8:
You are running at desired capacity of 3 and the maximum capacity of 3. You have alarms set at 60% CPU to scale out your application. Your application is now running at 80% capacity. What will happen?
A: Nothing
  The capacity of your ASG cannot go over the maximum capacity you have allocated during scale out events

Question 9:
I have an ASG and an ALB, and I setup my ASG to get health status of instances thanks to my ALB. One instance has just been reported unhealthy. What will happen?
A: The ASG will terminate the EC2 instance.
  Because the ASG has been configured to leverage the ALB health checks, unhealthy instances will be terminated

Question 10:
Your boss wants to scale your ASG based on the number of requests per minute your application makes to your database.
A: You create a CloudWatch custom metric and build an alarm on this to scale your ASG
  The metric "requests per minute" is not an AWS metric, hence it needs to be a custom metric

Question 11:
Scaling an instance from an r4.large to an r4.4xlarge is called
A: Vertical

Question 12:
Running an application on an auto scaling group that scales the number of instances in and out is called
A: Horizontal Scalability

Question 13:
You would like to expose a fixed static IP to your end-users for compliance purposes, so they can write firewall rules that will be stable and approved by regulators. Which Load Balancer should you use?
A: Network Load Balancer
  Network Load Balancers expose a public static IP, whereas an Application or Classic Load Balancer exposes a static DNS (URL)

Question 14:
A web application hosted in EC2 is managed by an ASG. You are exposing this application through an Application Load Balancer. The ALB is deployed on the VPC with the following CIDR: 192.168.0.0/18. How do you configure the EC2 instance security group to ensure only the ALB can access the port 80?
A: Open up the EC2 security on port 80 to the ALB's security group
  This is the most secure way of ensuring only the ALB can access the EC2 instances. Referencing by security groups in rules is an extremely powerful rule and many questions at the exam rely on it. Make sure you fully master the concepts behind it!

Question 15:
Your application load balancer is hosting 3 target groups with hostnames being users.example.com, api.external.example.com and checkout.example.com. You would like to expose HTTPS traffic for each of these hostnames. How do you configure your ALB SSL certificates to make this work?
A: Use SNI
  SNI (Server Name Indication) is a feature allowing you to expose multiple SSL certs if the client supports it. Read more here: https://aws.amazon.com/blogs/aws/new-application-load-balancer-sni/

Question 16:
An ASG spawns across 2 availability zones. AZ-A has 3 EC2 instances and AZ-B has 4 EC2 instances. The ASG is about to go into a scale-in event. What will happen?
A: Make sure you remember the Default Termination Policy for ASG. It tries to balance across AZ first, and then delete based on the age of the launch configuration.

Question 17:
The Application Load Balancers target groups can be all of these EXCEPT...
A: Network Load Balancer

Question 18:
You are running an application in 3 AZ, with an Auto Scaling Group and a Classic Load Balancer. It seems that the traffic is not evenly distributed amongst all the backend EC2 instances, with some AZ being overloaded. Which feature should help distribute the traffic across all the available EC2 instances?
A: Cross Zone Load Balancing

Question 19:
Your Application Load Balancer (ALB) currently is routing to two target groups, each of them is routed to based on hostname rules. You have been tasked with enabling HTTPS traffic for each hostname and have loaded the certificates onto the ALB. Which ALB feature will help it choose the right certificate for your clients?
A: Server Name Indication (SNI)

Question 20:
An application is deployed with an Application Load Balancer and an Auto Scaling Group. Currently, the scaling of the Auto Scaling Group is done manually and you would like to define a scaling policy that will ensure the average number of connections to your EC2 instances is averaging at around 1000. Which scaling policy should you use?
A: Target Tracking

-----------

-----------



## EBS & EFS

What’s an EBS Volume?
- An EC2 machine loses its root volume (main drive) when it is manually terminated.
- Unexpected terminations might happen from time to time (AWS would email you)
- Sometimes, you need a way to store your instance data somewhere

- An EBS **(Elastic Block Store) Volume** is a **network** drive you can attach to your instances while they run
- It allows your instances to persist data Amazon EBS

### EBS Volume
- **It’s a network drive** (i.e. not a physical drive)
  - It uses the network to communicate the instance, which means there might be a bit of latency
  - It __can be detached from an EC2 instance and attached to another one quickly__.

- **It’s locked to an Availability Zone (AZ)**
  - An EBS Volume in us-east-1a cannot be attached to us-east-1b
  - To move a volume across, you first need to snapshot it

- Have a provisioned capacity (size in GBs, and IOPS)
  - You get billed for all the provisioned capacity
  - You can increase the capacity of the drive over time

### EBS Volume Types
- EBS Volumes come in 4 types
  - **GP2 (SSD)**: General purpose SSD volume that balances price and performance for a wide variety of workloads
  - **IO1 (SSD)**: Highest-performance SSD volume for mission-critical low-latency or high- throughput workloads
  - **ST1 (HDD)**: Low cost HDD volume designed for frequently accessed, throughput- intensive workloads
  - **SC1 (HDD)**: Lowest cost HDD volume designed for less frequently accessed workloads

- EBS Volumes are characterized in Size | Throughput | IOPS (I/O Ops Per Sec)
- When in doubt always consult the AWS documentation – it’s good!
- **Only GP2 and IO1 can be used as boot volumes**



$ lsblk
$ sudo file -s /dev/xvdb
/dev/xvdb: data
$ sudo mkfs -t ext4 /dev/xvdb
mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
131072 inodes, 524288 blocks
26214 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=536870912
16 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912

Allocating group tables: done
Writing inode tables: done
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done

[ec2-user@ip-172-31-15-70 ~]$ sudo mkdir /mnt/data
[ec2-user@ip-172-31-15-70 ~]$ sudo mount /dev/xvdb /mnt/data/
[ec2-user@ip-172-31-15-70 ~]$ lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk
└─xvda1 202:1    0   8G  0 part /
xvdb    202:16   0   2G  0 disk /mnt/data

## EBS Volume Types Use cases GP2 (from AWS doc)
- Recommended for most workloads
- System boot volumes
- Virtual desktops
- Low-latency interactive apps
- Development and test environments

- 1 GiB - 16 TiB
- Small gp2 volumes can burst IOPS to 3000
- Max IOPS is 16,000…
- 3 IOPS per GB, means at 5,334GB we are at the max IOPS

## EBS Volume Types Use cases
**IO1 (from AWS doc)**
- Critical business applications that require sustained IOPS performance, or
more than 16,000 IOPS per volume (gp2 limit)
- Large database workloads, such as:
- MongoDB, Cassandra, Microsoft SQL Server, MySQL, PostgreSQL, Oracle

- 4 GiB - 16 TiB
- IOPS is provisioned (PIOPS) – MIN 100 - MAX 64,000 (Nitro instances) else MAX 32,000 (other instances)
- The maximum ratio of provisioned IOPS to requested volume size (in GiB) is 50:1

## EBS Volume Types Use cases
**ST1 (from AWS doc)**
- Streaming workloads requiring consistent, fast throughput at a low price.
- Big data, Data warehouses, Log processing
- Apache Kafka
- Cannot be a boot volume

- 500 GiB - 16 TiB
- Max IOPS is 500
- Max throughput of 500 MiB/s – can burst

## EBS Volume Types Use cases
**SC1 (from AWS doc)**
- Throughput-oriented storage for large volumes of data that is
infrequently accessed
- Scenarios where the lowest storage cost is important
- Cannot be a boot volume

- 500 GiB - 16 TiB
- Max IOPS is 250
- Max throughput of 250 MiB/s – can burst

## EBS –Volume Types Summary
- **gp2: General Purpose Volumes (cheap)**
  - 3 IOPS / GiB, minimum 100 IOPS, burst to 3000 IOPS, max 16000 IOPS
  - 1 GiB – 16 TiB , +1 TB = +3000 IOPS
- **io1: Provisioned IOPS (expensive)**
  - Min 100 IOPS, Max 64000 IOPS (Nitro) or 32000 (other)
  - 4 GiB - 16 TiB. Size of volume and IOPS are independent
- **st1: Throughput Optimized HDD**
  - 500 GiB – 16 TiB , 500 MiB /s throughput
- **sc1: Cold HDD, Infrequently accessed data**
  - 500 GiB – 16 TiB , 250 MiB /s throughput

## EBS Snapshots
- **Incremental – only backup changed blocks** [*]
- EBS backups use IO and you shouldn’t run them while your application is handling a lot of traffic
- Snapshots will be stored in S3 (but you won’t directly see them)
- Not necessary to detach volume to do snapshot, but recommended
- Max 100,000 snapshots
- Can copy snapshots across AZ or Region
- Can make Image (AMI) from Snapshot
- **EBS volumes restored by snapshots need to be pre-warmed (using fio or dd command to read the entire volume)**
- **Snapshots can be automated using Amazon Data Lifecycle Manager**

Tip: Use "Create Snapshot Lifecycle Policy" for backups

## EBS Migration
- EBS Volumes are only locked to a specific AZ
- To migrate it to a different AZ (or region):
  - Snapshot the volume
  - (optional) Copy the volume to a different region
  - Create a volume from the snapshot in the AZ of your choice

- Let’s practice!

## EBS Encryption
- When you create an encrypted EBS volume, you get the following:
  - Data at rest is encrypted inside the volume
  - All the data in flight moving between the instance and the volume is encrypted
  - All snapshots are encrypted
  - All volumes created from the snapshot
- Encryption and decryption are handled transparently (you have nothing to do)
- Encryption has a minimal impact on latency
- EBS Encryption leverages keys from KMS (AES-256)
- Copying an unencrypted snapshot allows encryption
- Snapshots of encrypted volumes are encrypted

### Encryption: encrypt an unencrypted EBS volume
- Create an EBS snapshot of the volume
- Encrypt the EBS snapshot ( using copy )
- Create new ebs volume from the snapshot ( the volume will also be encrypted )
- Now you can attach the encrypted volume to the original instance

## EBS vs Instance Store
- Some instance do not come with Root EBS volumes
- Instead, they come with “Instance Store” (= ephemeral storage)
- Instance store is physically attached to the machine (EBS is a network drive)
- Pros:
  - Better I/O performance (EBS gp2 has an max IOPS of 16000, io1 of 64000)
  - Good for buffer / cache / scratch data / temporary content
  - Data survives reboots
- Cons:
  - On stop or termination, the instance store is lost
  - You can’t resize the instance store
  - Backups must be operated by the user

## Local EC2 Instance Store
- **Physical disk attached to the physical server where your EC2 is**
- Very High IOPS (because physical)
- Disks up to 7.5 TiB (can change over time), stripped to reach 30 TiB (can change over time…)
- Block Storage (just like EBS)
- Cannot be increased in size
- Risk of data loss if hardware fails

## EBS RAID Options
- **EBS is already redundant storage** (replicated within an AZ)
- But what if you want to increase IOPS to say 100 000 IOPS?
- What if you want to mirror your EBS volumes?
- You would mount volumes in parallel in RAID settings!
- RAID is possible as long as your OS supports it
- Some RAID options are:
  - RAID 0
  - RAID 1
  - RAID 5 (not recommended for EBS – see documentation)
  - RAID 6 (not recommended for EBS – see documentation)
- We’ll explore RAID 0 and RAID 1

### RAID 0 (increase performance) [*]
- Combining 2 or more volumes and getting the total disk space and I/O
- But one disk fails, all the data is failed
- Use cases would be:
  - An application that needs a lot of IOPS and doesn’t need fault-tolerance
  - A database that has replication already built-in
- Using this, we can have a very big disk with a lot of IOPS
- For example
  - two 500 GiB Amazon EBS io1 volumes with 4,000 provisioned IOPS each will create a…
  - 1000 GiB RAID 0 array with an available bandwidth of 8,000 IOPS and 1,000 MB/s of throughput

### RAID 1 (increase fault tolerance)
- RAID 1 = Mirroring a volume to another
- If one disk fails, our logical volume is still working
- We have to send the data to two EBS volume at the same time (2x network)
- Use case:
  - Application that need increase volume fault tolerance
  - Application where you need to service disks
- For example:
  - two 500 GiB Amazon EBS io1 volumes with 4,000 provisioned IOPS each will create a…
  - 500 GiB RAID 1 array with an available bandwidth of 4,000 IOPS and 500 MB/s of throughput

## EFS – Elastic File System

- Managed NFS (network file system) that can be mounted on many EC2
- EFS works with EC2 instances in multi-AZ
- Highly available, scalable, expensive (3x gp2), pay per use

### EFS – Elastic File System
- Use cases: **content management, web serving, data sharing, Wordpress**
- Uses NFSv4.1 protocol
- Uses **security group** to control access to EFS
- **Compatible with Linux** based AMI (not Windows)
- Encryption at rest using KMS

- POSIX file system (~Linux) that has a standard file API
- File system scales automatically, pay-per-use, no capacity planning!

### EFS – Performance & Storage Classes [*]
- **EFS Scale**
  - 1000s of concurrent NFS clients, 10 GB+ /s throughput
  - Grow to Petabyte-scale network file system, automatically
- **Performance mode (set at EFS creation time)**
  - General purpose (default): latency-sensitive use cases (web server, CMS, etc…)
  - Max I/O – higher latency, throughput, highly parallel (big data, media processing)
- **Storage Tiers (lifecycle management feature – move file after N days)**
  - Standard: for frequently accessed files
  - Infrequent access (EFS-IA): cost to retrieve files, lower price to store


To set up your EC2 instance:

Using the Amazon EC2 console, associate your EC2 instance with a VPC security group that enables access to your mount target. For example, if you assigned the "default" security group to your mount target, you should assign the "default" security group to your EC2 instance. Learn more
Open an SSH client and connect to your EC2 instance. (Find out how to connect.)
If you're using an Amazon Linux EC2 instance, install the EFS mount helper with the following command:
sudo yum install -y amazon-efs-utils
You can still use the EFS mount helper if you're not using an Amazon Linux instance. Learn more

If you're not using the EFS mount helper, install the NFS client on your EC2 instance:
On a Red Hat Enterprise Linux or SUSE Linux instance, use this command:
sudo yum install -y nfs-utils
On an Ubuntu instance, use this command:
sudo apt-get install nfs-common
Mounting your file system

Open an SSH client and connect to your EC2 instance. (Find out how to connect).
Create a new directory on your EC2 instance, such as "efs".
sudo mkdir efs
Mount your file system with a method listed following. If you need encryption of data in transit, use the EFS mount helper and the TLS mount option. Mounting considerations
Using the EFS mount helper:
sudo mount -t efs fs-776c8b4f:/ efs
Using the EFS mount helper and the TLS mount option:
sudo mount -t efs -o tls fs-776c8b4f:/ efs
Using the NFS client:
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-776c8b4f.efs.ap-southeast-2.amazonaws.com:/ efs


## EBS vs EFS – Elastic Block Storage
- EBS volumes…
  - can be attached to **only one instance** at a time
  - are **locked at the Availability Zone** (AZ) level
  - gp2: IO increases if the disk size increases
  - io1: can increase IO independently
- To migrate an EBS volume across AZ
  - Take a snapshot
  - Restore the snapshot to another AZ
  - EBS backups use IO and you shouldn’t run them while your application is handling a lot of traffic
- Root EBS Volumes of instances get terminated by default if the EC2 instance gets terminated.

**EBS vs EFS – Elastic File System**
- Mounting 100s of instances across AZ
- EFS share website files (WordPress)
- Only for Linux Instances (POSIX)

- EFS has a higher price point than EBS
- Can leverage EFS-IA for cost savings

- Remember: EFS vs EBS vs Instance Store

---

EC2 Data Management - EBS & EFS Quiz

---

Question 1:
Your instance in us-east-1a just got terminated, and the attached EBS volume is now available. Your colleague tells you he can't seem to attach it to your instance in us-east-1b.
A: EBS volumes are AZ locked
  EBS Volumes are created for a specific AZ. It is possible to migrate them between different AZ through backup and restore

Question 2:
You have provisioned an 8TB gp2 EBS volume and you are running out of IOPS. What is NOT a way to increase performance?
A: Increase the EBS volume size.
  EBS IOPS peaks at 16,000 IOPS. or equivalent 5334 GB.

Question 3:
You would like to leverage EBS volumes in parallel to linearly increase performance, while accepting greater failure risks. Which RAID mode helps you in achieving that?
A: RAID 0
  See https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/raid-config.html

Question 4:
Although EBS is already a replicated solution, your company SysOps advised you to use a RAID mode that will mirror data and will allow your instance to not be affected if an EBS volume entirely fails. Which RAID mode did he recommend to you?
A: RAID 1
  See https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/raid-config.html


Question 5:
You would like to have the same data being accessible as an NFS drive cross AZ on all your EC2 instances. What do you recommend?
  EFS is a network file system (NFS) and allows to mount the same file system on EC2 instances that are in different AZ

Question 6:
You would like to have a high-performance cache for your application that mustn't be shared. You don't mind losing the cache upon termination of your instance. Which storage mechanism do you recommend as a Solution Architect?
A: Instance Store
  Instance Store provide the best disk performance

Question 7:
You are running a high-performance database that requires an IOPS of 210,000 for its underlying filesystem. What do you recommend?
A: Use EC2 Instance Store
  Is running a DB on EC2 instance store possible? It is possible to run a database on EC2. It is also possible to use instance store, but there are some considerations to have. The data will be lost if the instance is stopped, but it can be restarted without problems. One can also set up a replication mechanism on another EC2 instance with instance store to have a standby copy. One can also have back-up mechanisms. It's all up to how you want to set up your architecture to validate your requirements. In this case, it's around IOPS, and we build an architecture of replication and back up around i

-----

## RDS, Aurora & ElastiCache

### AWS RDS Overview
- RDS stands for Relational Database Service
- It’s a managed DB service for DB use SQL as a query language.
- It allows you to create databases in the cloud that are managed by AWS
  - Postgres
  - MySQL
  - MariaDB
  - Oracle
  - Microsoft SQL Server
  - Aurora (AWS Proprietary database)

### Advantage over using RDS versus deploying DB on EC2
- RDS is a managed service:
  - Automated provisioning, OS patching
  - Continuous backups and restore to specific timestamp (Point in Time Restore)!
  - Monitoring dashboards
  - Read replicas for improved read performance
  - Multi AZ setup for DR (Disaster Recovery)
  - Maintenance windows for upgrades
  - Scaling capability (vertical and horizontal)
  - Storage backed by EBS (gp2 or io1)
- BUT you can’t SSH into your instances

### RDS Backups
- Backups are automatically enabled in RDS
- Automated backups:
  - Daily full backup of the database (during the maintenance window)
  - Transaction logs are backed-up by RDS every 5 minutes
  - => ability to restore to any point in time (from oldest backup to 5 minutes ago)
  - 7 days retention (can be increased to 35 days)
- DB Snapshots:
  - Manually triggered by the user
  - Retention of backup for as long as you want

### RDS Read Replicas for read scalability [*]
- Up to 5 Read Replicas
- Within AZ, Cross AZ or Cross Region
- Replication is **ASYNC**, so reads are eventually consistent
- Replicas can be promoted to their own DB
- Applications must update the connection string to leverage read replicas

### RDS Read Replicas – Use Cases [*]
- You have a production database that is taking on normal load
- You want to run a reporting application to run some analytics
- You create a Read Replica to run the new workload there
- The production application is unaffected
- Read replicas are used for SELECT (=read) only kind of statements (not INSERT, UPDATE, DELETE)

### RDS Read Replicas – Network Cost
- In AWS there’s a network cost when data goes from one AZ to another.
- To reduce the cost, you can have your Read Replicas in the same AZ

### RDS Multi AZ (Disaster Recovery)
- **SYNC** replication
- One DNS name – automatic app failover to standby
- Increase **availability**
- Failover in case of loss of AZ, loss of network, instance or storage failure
- No manual intervention in apps
- Not used for scaling
- __Note__: **The Read Replicas be setup as Multi AZ for Disaster Recovery (DR)** [*]

### RDS Security - Encryption
- At rest encryption
  - Possibility to encrypt the master & read replicas with AWS KMS - AES-256 encryption
  - Encryption has to be defined at launch time
  - **If the master is not encrypted, the read replicas __cannot__ be encrypted** [*]
  - Transparent Data Encryption (TDE) available for Oracle and SQL Server

- In-flight encryption
  - SSL certificates to encrypt data to RDS in flight
  - Provide SSL options with trust certificate when connecting to database
  - To enforce SSL:
    - PostgreSQL: rds.force_ssl=1 in the AWS RDS Console (Parameter Groups)
    - MySQL: Within the DB: GRANT USAGE ON *.* TO 'mysqluser'@'%' REQUIRE SSL;

### RDS Encryption Operations
- **Encrypting RDS backups**
  - Snapshots of un-encrypted RDS databases are un-encrypted
  - Snapshots of encrypted RDS databases are encrypted
  - __Can copy a snapshot into an encrypted one__

- **To encrypt an un-encrypted RDS database:**
  - Create a snapshot of the un-encrypted database
  - Copy the snapshot and enable encryption for the snapshot
  - Restore the database from the encrypted snapshot
  - Migrate applications to the new database, and delete the old database

### RDS Security – Network & IAM
- Network Security
  - RDS databases are usually deployed __within a private subnet__, not in a public one
  - RDS security works by leveraging security groups (the same concept as for EC2 instances) – it controls which IP / security group can **communicate** with RDS

- Access Management
  - IAM policies help control who can **manage** AWS RDS (through the RDS API)
  - Traditional Username and Password can be used to **login** into the database
  - **IAM-based authentication can be used to login into RDS MySQL & PostgreSQL**

### RDS - IAM Authentication
- IAM database authentication works with **MySQL and PostgreSQL**
- You don’t need a password, just an authentication token obtained through IAM & RDS API calls
- Auth token has a lifetime of 15 minutes

- Benefits:
  - Network in/out must be encrypted using SSL
  - IAM to centrally manage users instead of DB
  - Can leverage IAM Roles and EC2 Instance

### RDS Security – Summary
- Encryption at rest:
  - Is done only when you first create the DB instance
  - or: unencrypted DB => snapshot => copy snapshot as encrypted => create DB from snapshot
- Your responsibility:
  - Check the ports / IP / security group inbound rules in DB’s SG
  - In-database user creation and permissions or manage through IAM
  - Creating a database with or without public access
  - Ensure parameter groups or DB is configured to only allow SSL connections
- AWS responsibility:
  - No SSH access
  - No manual DB patching
  - No manual OS patching
  - No way to audit the underlying instance

## Amazon Aurora [*] Exam many question
- Aurora is a proprietary technology from AWS (not open sourced)
- Postgres and MySQL are both supported as Aurora DB (that means your drivers will work as if Aurora was a Postgres or MySQL database)
- Aurora is “AWS cloud optimized” and claims 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
- Aurora storage automatically grows in increments of 10GB, up to 64 TB.
- Aurora can have 15 replicas while MySQL has 5, and the replication process is faster (sub 10 ms replica lag)
- Failover in Aurora is instantaneous. It’s HA (High Availability) native.
- Aurora costs more than RDS (20% more) – but is more efficient

### Aurora High Availability and Read Scaling
- 6 copies of your data across 3 AZ:
  - 4 copies out of 6 needed for writes
  - 3 copies out of 6 need for reads
  - Self healing with peer-to-peer replication
  - Storage is striped across 100s of volumes
- One Aurora Instance takes writes (master)
- Automated failover for master in less than 30 seconds
- Master + up to 15 Aurora Read Replicas serve reads
- Support for Cross Region Replication Shared storage Volume

**Replication + Self Healing + Auto Expanding**

### Aurora DB Cluster
Shared storage Volume
Auto Expanding from 10G to 64 TB

Reader Endpoint Connection LB

### Features of Aurora
- Automatic fail-over
- Backup and Recovery
- Isolation and security
- Industry compliance
- Push-button scaling
- Automated Patching with Zero Downtime
- Advanced Monitoring
- Routine Maintenance
- Backtrack: restore data at any point of time without using backups

### Aurora Security
- Similar to RDS because uses the same engines
- Encryption at rest using KMS
- Automated backups, snapshots and replicas are also encrypted
- Encryption in flight using SSL (same process as MySQL or Postgres)
- ** **
- You are responsible for protecting the instance with security groups
- You can’t SSH


### Aurora Serverless
- Automated database instantiation and auto
- **scaling based on actual usage**
- **Good for infrequent, intermittent or unpredictable workloads**
- No capacity planning needed
- Pay per second, can be more cost-effective

### Global Aurora
- Aurora Cross Region Read Replicas:
  - Useful for disaster recovery
  - Simple to put in place
- **Aurora Global Database (recommended)**:
  - 1 Primary Region (read / write)
  - Up to 5 secondary (read-only) regions, replication lag is less than 1 second
  - Up to 16 Read Replicas per secondary region
  - Helps for decreasing latency
  - Promoting another region (for disaster recovery) has an RTO of < 1 minute

dev/test db.t2.small

### Amazon ElastiCache Overview
- The same way RDS is to get managed Relational Databases…
- ElastiCache is to get managed Redis or Memcached
- Caches are in-memory databases with really high performance, low latency
- Helps reduce load off of databases for read intensive workloads
- Helps make your application stateless
- Write Scaling using sharding
- Read Scaling using REad Replicas
- Multi AZ with Failover Replicas.
- AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups
- **__Using ElastiCache involves heavy application code changes__**

## ElastiCache
Solution Architecture - DB Cache
- Applications queries ElastiCache, if not available, get from RDS and store in ElastiCache.
- Helps relieve load in RDS
- Cache must have an invalidation strategy to make sure only the most current data

### Solution Architecture – User Session Store
- User logs into any of the application
- The application writes the session data into ElastiCache
- The user hits another instance of our application
- The instance retrieves the data and the user is already logged in

### ElastiCache – Redis vs Memcached
**REDIS**
- **Multi AZ** with Auto-Failover
- **Read Replicas** to scale reads and have **high availability**
- Data Durability using AOF persistence
- **Backup and restore features**
**MEMCACHED**
- Multi-node for partitioning of data (sharding)
- **Non persistent**
- **No backup and restore**
- Multi-threaded architecture
+ Replication

### ElastiCache – Cache Security
- All caches in ElastiCache:
  - Support SSL in flight encryption
  - **__Do not support IAM authentication__**
  - IAM policies on ElastiCache are only used for AWS API-level security
- **Redis AUTH**
  - You can set a “password/token” when you create a Redis cluster
  - This is an extra level of security for your cache (on top of security groups)
- Memcached
  - Supports SASL-based authentication (advanced)

### ElastiCache for Solutions Architects
- Patterns for ElastiCache
  - **Lazy Loading**: all the read data is cached, data can become stale in cache
  - **Write Through**: Adds or update data in the cache when written to a DB (no stale data)
  - **Session Store**: store temporary session data in a cache (using TTL features)

- Quote: There are only two hard things in Computer Science: cache invalidation and naming things

-----

RDS / Aurora / ElastiCache Quiz

Quiz 5

Question 1:
My company would like to have a MySQL database internally that is going to be available even in case of a disaster in the AWS Cloud. I should setup
A: Multi AZ

  In this question, we consider a disaster to be an entire Availability Zone going down. In which case Multi-AZ will help. If we want to plan against an entire region going down, backups and replication across regions would help.

Question 2:
Our RDS database struggles to keep up with the demand of the users from our website. Our million users mostly read news, and we don't post news very often. Which solution is NOT adapted to this problem?
A:   An ElasticCache Cluster
     RDS Read Replicas
  -  Multi AZ

  Be very careful with the way you read questions at the exam. Here, the question is asking which solution is NOT adapted to this problem. ElastiCache and RDS Read Replicas do indeed help with scaling reads.

Question 3:
We have setup read replicas on our RDS database, but our users are complaining that upon updating their social media posts, they do not see the update right away
A: Read Replicas have asynchronous replication and therefore it's likely our users will only observe eventual consistency

Question 4:
Which RDS Classic (not Aurora) feature does not require us to change our SQL connection string?
A: Multi AZ

  Multi AZ keeps the same connection string regardless of which database is up. Read Replicas imply we need to reference them individually in our application as each read replica will have its own DNS name

Question 5:
You want to ensure your Redis cluster will always be available
A: X Enable Read Replicas
   - Enable Multi AZ

   Multi AZ ensures high availability

Question 6:
Your application functions on an ASG behind an ALB. Users have to constantly log back in and you'd rather not enable stickiness on your ALB as you fear it will overload some servers. What should you do?
A: Store session data in ElasticCache.

  Storing Session Data in ElastiCache is a common pattern to ensuring different instances can retrieve your user's state if needed.

Question 7:
One analytics application is currently performing its queries against your main production database. These queries slow down the database which impacts the main user experience. What should you do to improve the situation?
A: Setup a Read Replicas

  Read Replicas will help as our analytics application can now perform queries against it, and these queries won't impact the main production database.

Question 8:
You have a requirement to use TDE (Transparent Data Encryption) on top of KMS. Which database technology does NOT support TDE on RDS?
A: PostgreSQL

Question 9:
Which RDS database technology does NOT support IAM authentication?
A: Oracle

Question 10:
You would like to ensure you have a database available in another region if a disaster happens to your main region. Which database do you recommend?
A: Aurora Global Database

  Global Databases allow you to have cross region replication

Question 11:
How can you enhance the security of your Redis cache to force users to enter a password?
A: Use Redis AUTH

Question 12:
[SAA-C02] Your company has a production Node.js application that is using RDS MySQL 5.6 as its data backend. A new application programmed in Java will perform some heavy analytics workload to create a dashboard, on a regular hourly basis. You want to the final solution to minimize costs and have minimal disruption on the production application, what should you do?
A: Create a Read Replica in the same AZ and run the analytics workload on the replica database

  this will minimize cost because the data won't have to move across AZ

Question 13:
[SAA-C02] You would like to create a disaster recovery strategy for your RDS PostgreSQL database so that in case of a regional outage, a database can be quickly made available for Read and Write workload in another region. The DR database must be highly available. What do you recommend?
A: Create a RR in a different region and enable multi-AZ on the main database.

Question 14:
You are managing a PostgreSQL database and for security reasons, you would like to ensure users are authenticated using short-lived credentials. What do you suggest doing?
A: Use PostgreSQL for RDS and authenticate using a token obtained through the RDS service.

  In this case, IAM is leveraged to obtain the RDS service token, so this is the IAM authentication use case.

[SAA-C02] An application is running in production, using an Aurora database as its backend. Your development team would like to run a version of the application in a scaled-down application, but still, be able to perform some heavy workload on a need-basis. Most of the time, the application will be unused. Your CIO has tasked you with helping the team while minimizing costs. What do you suggest?
A:


-----

[SAA-C02] List of Ports to be familiar with
Here's a list of standard ports you should see at least once. You shouldn't remember them (the exam will not test you on that), but you should be able to differentiate between an Important (HTTPS - port 443) and a database port (PostgreSQL - port 5432)

Important ports:

FTP: 21
SSH: 22
SFTP: 22 (same as SSH)
HTTP: 80
HTTPS: 443

vs RDS Databases ports:

PostgreSQL: 5432
MySQL: 3306
Oracle RDS: 1521
MSSQL Server: 1433
MariaDB: 3306 (same as MySQL)

Aurora: 5432 (if PostgreSQL compatible) or 3306 (if MySQL compatible)

Don't stress out on remember those, just read that list once today and once before going into the exam and you should be all set :)

Remember, you should just be able to differentiate an "Important Port" vs an "RDS database Port".

----


## Route 53 Section
- TTL
- CNAME vs Alias
- Health Checks
- Routing Policies
  - Simple
  - Weighted
  - Latency
  - Failover
  - Geolocation
  - Multi Value
- 3rd party domains integration

### AWS Route 53 Overview
- Route53 is a Managed DNS (Domain Name System)
- DNS is a collection of rules and records which helps clients understand how to reach a server through URLs.
- In AWS, the most common records are:
  - A: hostname to IPv4
  - AAAA: hostname to IPv6
  - CNAME: hostname to hostname
  - Alias: hostname to AWS resource.

### AWS Route 53 Overview
- Route53 can use:
- public domain names you own (or buy)
application1.mypublicdomain.com
- private domain names that can be resolved by your instances in your VPCs.
application1.company.internal
- Route53 has advanced features such as:
- Load balancing (through DNS – also called client load balancing)
- Health checks (although limited…)
- Routing policy: simple, failover, geolocation, latency, weighted, multi value
- You pay $0.50 per month per hosted zone

### DNS Records TTL (Time to Live)

- **High TTL: (e.g. 24hr)**
  - Less traffic on DNS
  - Possibly outdated records
- **Low TTL: (e.g 60 s)**
  - More traffic on DNS
  - Records are outdated for less time
  - Easy to change records

- **TTL is mandatory for each DNS record**

### CNAME vs Alias [*]
- AWS Resources (Load Balancer, CloudFront…) expose an AWS hostname:
***lb1-1234.us-east-2.elb.amazonaws.com*** and you want ***myapp.mydomain.com***
- CNAME:
  - Points a hostname to any other hostname. (app.mydomain.com => blabla.anything.com)
  - ***ONLY FOR NON ROOT DOMAIN (aka. something.mydomain.com)***
- Alias:
  - Points a hostname to an AWS Resource (app.mydomain.com => blabla.amazonaws.com)
  - ***Works for ROOT DOMAIN and NON ROOT DOMAIN (aka mydomain.com)***
  - Free of charge
  - Native health check

### Simple Routing Policy
- Maps a hostname to another hostname
- Use when you need to redirect to a single resource
- You can’t attach health checks to simple routing policy
- If multiple values are returned, a random one is chosen by the client

### Weighted Routing Policy
- Control the % of the requests that go to specific endpoint
- Helpful to test 1% of traffic on new app version for example
- Helpful to split traffic between two regions
- Can be associated with Health Checks

### Latency Routing Policy
- Redirect to the server that has the least latency close to us
- Super helpful when latency of users is a priority
- **Latency is evaluated in terms of user to designated AWS Region**
- Germany may be directed to the US (if that’s the lowest latency)

### Health Checks
- Have X health checks failed => unhealthy (default 3)
- After X health checks passed => health (default 3)
- Default Health Check Interval: 30s (can set to 10s – higher cost)
- About 15 health checkers will check the endpoint health
- => one request every 2 seconds on average
- Can have HTTP, TCP and HTTPS health checks (no SSL verification)
- Possibility of integrating the health check with CloudWatch

- **Health checks can be linked to Route53 DNS queries!**

### Geo Location Routing Policy
- Different from Latency based!
- **This is routing based on user location**
- Here we specify: traffic from the UK should go to this specific IP
- Should create a “default” policy (in case there’s no match on location)

### Multi Value Routing Policy
- Use when routing traffic to multiple resources
- Want to associate a Route 53 health checks with records
- Up to 8 healthy records are returned for each Multi Value query
- ***Multi Value is not a substitute for having an ELB***

### Route53 as a Registrar
- A domain name registrar is an organization that manages the
reservation of Internet domain names
- Famous names:
- GoDaddy
- Google Domains
- Etc…
- And also… Route53 (e.g. AWS)!
- **Domain Registrar != DNS**

### 3rd Party Registrar with AWS Route 53
- **If you buy your domain on 3rd party website, you can still use Route53**.

- 1) Create a Hosted Zone in Route 53
- 2) Update NS Records on 3rd party website to use Route 53 **name servers**

- **Domain Registrar != DNS**
- (But each domain registrar usually comes with some DNS features)


-----

Question 1:
You have purchased "mycoolcompany.com" on the AWS registrar and would like for it to point to lb1-1234.us-east-2.elb.amazonaws.com . What sort of Route 53 record is NOT POSSIBLE to set up for this?
A: CNAME

  The DNS protocol does not allow you to create a CNAME record for the top node of a DNS namespace (mycoolcompany.com), also known as the zone apex

Question 2:
You have deployed a new Elastic Beanstalk environment and would like to direct 5% of your production traffic to this new environment, in order to monitor for CloudWatch metrics and ensuring no bugs exist. What type of Route 53 records allows you to do so?
A: Weighted

  Weighted allows you to redirect a part of the traffic based on a weight (hence a percentage). It's common to use to send a part of a traffic to a new application you're deploying

Question 3:
After updating a Route 53 record to point "myapp.mydomain.com" from an old Load Balancer to a new load balancer, it looks like the users are still not redirected to your new load balancer. You are wondering why...
A: It's because of the TTL

  DNS records have a TTL (Time to Live) in order for clients to know for how long to caches these values and not overload the DNS with DNS requests. TTL should be set to strike a balance between how long the value should be cached vs how much pressure should go on the DNS.

Question 4:
You want your users to get the best possible user experience and that means minimizing the response time from your servers to your users. Which routing policy will help?
A: Latency

  Latency will evaluate the latency results and help your users get a DNS response that will minimize their latency (e.g. response time)

Question 5:
You have a legal requirement that people in any country but France should not be able to access your website. Which Route 53 record helps you in achieving this?
A: Geolocation

Question 6:
You have purchased a domain on Godaddy and would like to use it with Route 53. What do you need to change to make this work?
A: Create a public hosted zone and update the 3rd party registrar NS records

  Private hosted zones are meant to be used for internal network queries and are not publicly accessible. Public Hosted Zones are meant to be used for people requesting your website through the public internet. Finally, NS records must be updated on the 3rd party registrar.




-----


## Classic Solutions Architecture

### Section Introduction
- These solutions architectures are the best part of this course
- Let’s understand how all the technologies we’ve seen work together
- This is a section you need to be 100% comfortable with

- We’ll see the progression of a Solution’s architect mindset through many sample case studies:
  - WhatIsTheTime.Com
  - MyClothes.Com
  - MyWordPress.Com
  - Instantiating applications quickly
  - Beanstalk

### Stateless Web App: WhatIsTheTime.com
- WhatIsTheTime.com allows people to know what time it is
- We don’t need a database
- We want to start small and can accept downtime
- We want to fully scale vertically and horizontally, no downtime
- Let’s go through the Solutions Architect journey for this app

- Let’s see how we can proceed!

#### In this lecture we’ve discussed…
- Public vs Private IP and EC2 instances
- Elastic IP vs Route 53 vs Load Balancers
- Route 53 TTL, A records and Alias Records
- Maintaining EC2 instances manually vs Auto Scaling Groups
- Multi AZ to survive disasters
- ELB Health Checks
- Security Group Rules
- Reservation of capacity for costing savings when possible
- We’re considering 5 pillars for a well architected application:
  - costs,
  - performance,
  - reliability,
  - security,
  - operational excellence


### Stateful Web App: MyClothes.com
- MyClothes.com allows people to buy clothes online.
- There’s a shopping cart
- Our website is having hundreds of users at the same time
- We need to scale, maintain horizontal scalability and keep our web application as stateless as possible
- Users should not lose their shopping cart
- Users should have their details (address, etc) in a database

### In this lecture we’ve discussed…
**3-tier architectures for web applications**
- ELB sticky sessions
- Web clients for storing cookies and making our web app stateless
- ElastiCache
  - For storing sessions (alternative: DynamoDB)
  - For caching data from RDS
  - Multi AZ
- RDS
  - For storing user data
  - Read replicas for scaling reads
  - Multi AZ for disaster recovery
- Tight Security with security groups referencing each other


### Stateful Web App: MyWordPress.com
- We are trying to create a fully scalable WordPress website
- We want that website to access and correctly display picture uploads
- Our user data, and the blog content should be stored in a MySQL database.

In this lecture we’ve discussed… - Aurora Database to have easy Multi-AZ and Read
-Replicas
- Storing data in EBS (single instance application) - Vs Storing data in EFS (distributed application)

## Instantiating Applications quickly
- When launching a full stack (EC2, EBS, RDS), it can take time to:
  - Install applications
  - Insert initial (or recovery) data
  - Configure everything
  - Launch the application

- We can take advantage of the cloud to speed that up!

## Instantiating Applications quickly
- EC2 Instances:
  - **Use a Golden AMI**: Install your applications, OS dependencies etc.. beforehand and launch your EC2 instance from the Golden AMI
  - **Bootstrap using User Data**: For dynamic configuration, use User Data scripts
  - **Hybrid**: mix Golden AMI and User Data (Elastic Beanstalk)
- RDS Databases:
  - Restore from a snapshot: the database will have schemas and data ready!
- EBS Volumes:
  - Restore from a snapshot: the disk will already be formatted and have data!

### Developer problems on AWS
- Managing infrastructure
- Deploying Code
- Configuring all the databases, load balancers, etc
- Scaling concerns

- Most web apps have the same architecture (ALB + ASG)
- All the developers want is for their code to run!
- Possibly, consistently across different applications and environments


## AWS Elastic Beanstalk Overview
- Elastic Beanstalk is a developer centric view of deploying an application
on AWS

- It uses all the component’s we’ve seen before:
  EC2, ASG, ELB, RDS, etc…
- But it’s all in one view that’s easy to make sense of!
- We still have full control over the configuration

- Beanstalk is free but you pay for the underlying instances

### Elastic Beanstalk
- Managed service
  - Instance configuration / OS is handled by Beanstalk
  - Deployment strategy is configurable but performed by Elastic Beanstalk

- Just the application code is the responsibility of the developer

- Three architecture models:
  - Single Instance deployment: good for dev
  - LB + ASG: great for production or pre-production web applications
  - ASG only: great for non-web apps in production (workers, etc..)

### Elastic Beanstalk
  - Elastic Beanstalk has three components
  - Application
  - Application version: each deployment gets assigned a version

- Environment name (dev, test, prod…): free naming
- You deploy application versions to environments and can promote application
versions to the next environment
- Rollback feature to previous application version
- Full control over lifecycle of environments

### Elastic Beanstalk
- Support for many platforms:
  - Go
  - Java SE
  - Java with Tomcat
  - .NET on Windows Server with IIS
  - Node.js
  - PHP
  - Python
  - Ruby
  - Packer Builder
  - Single Container Docker
  - Multicontainer Docker
  - Preconfigured Docker

- If not supported, you can write your custom platform (advanced)

-----

Question 1:
You have an ASG that scales on demand based on the traffic going to your new website: TriangleSunglasses.Com. You would like to optimise for cost, so you have selected an ASG that scales based on demand going through your ELB. Still, you want your solution to be highly available so you have selected the minimum instances to 2. How can you further optimize the cost while respecting the requirements?
A: Reserve two EC2 instances

  This is the way to save further costs as we know we will run 2 EC2 instances no matter what.

Question 2:
Which of the following will NOT help make our application tier stateless?
A: Storing shared data on EBS volumes

  EBS volumes are created for a specific AZ and can only be attached to one EC2 instance at a time. This will not help make our application stateles

Question 3:
You are looking to store shared software updates data across 100s of EC2 instances. The software updates should be dynamically loaded on the EC2 instances and shouldn't require heavy operations. What do you sugges
A: Store the software updates on EFS and mount EFS as a network drive

  EFS is a network file system (NFS) and allows to mount the same file system to 100s of EC2 instances. Publishing software updates their allow each EC2 instance to access them.

Question 4:
As a solution architect managing a complex ERP software suite, you are orchestrating a migration to the AWS cloud. The software traditionally takes well over an hour to setup on a Linux machine, and you would like to make sure your application does leverage the ASG feature of auto scaling based on the demand. How do you recommend you speed up the installation process?
A: Use a Golden AMI

  Golden AMI are a standard in making sure you snapshot a state after an application installation so that future instances can boot up from that AMI quickly.

Question 5:
I am creating an application and would like for it to be running with minimal cost in a development environment with Elastic Beanstalk. I should run it in
A: Single Instance Mode

  This will create one EC2 instance and one Elastic IP

Question 6:
My deployments on Elastic Beanstalk have been painfully slow, and after looking at the logs, I realize this is due to the fact that my dependencies are resolved on each EC2 machine at deployment time. How can I speed up my deployment with the minimal impact?
A: Create a Golden AMI that contains the dependencies and launch the EC2 instances from that.

  Golden AMI are a standard in making sure save the state after the installation or pulling dependencies so that future instances can boot up from that AMI quickly.

-----

## S3 Storage and Data Management

### Section introduction
- Amazon S3 is one of the main building blocks of AWS
- It’s advertised as **”infinitely scaling”** storage
- It’s widely popular and deserves its own section

- Many websites use Amazon S3 as a backbone
- Many AWS services uses Amazon S3 as an integration as well

- We’ll have a step-by-step approach to S3

### Amazon S3 Overview - Buckets
- Amazon S3 allows people to store objects (files) in “buckets” (directories)
- Buckets must have a **globally unique name**
- Buckets are defined at the **region level**
  - Naming convention
  - No uppercase
  - No underscore
  - 3-63 characters long
  - Not an IP
  - Must start with lowercase letter or number

## Amazon S3 Overview - Objects
- Objects (files) have a Key
- The **key** is the **FULL** path:
  - s3://my-bucket/my_file.txt
  - s3://my-bucket/my_folder1/another_folder/my_file.txt
- The key is composed of prefix + object name
  - s3://my-bucket/my_folder1/another_folder/my_file.txt
- There’s no concept of “directories” within buckets (although the UI will trick you to think otherwise)
- Just keys with very long names that contain slashes (“/”)

## Amazon S3 Overview – Objects (continued)
- Object values are the content of the body:
  - Max Object Size is 5TB (5000GB)
  - If uploading more than 5GB, must use “multi-part upload”

- Metadata (list of text key / value pairs – system or user metadata)
- Tags (Unicode key / value pair – up to 10) – useful for security / lifecycle
- Version ID (if versioning is enabled)

### Amazon S3 - Versioning
- You can version your files in Amazon S3
- It is enabled at the **bucket level**
- Same key overwrite will increment the “version”: 1, 2, 3….
- It is best practice to version your buckets
  - Protect against unintended deletes (ability to restore a version)
  - Easy roll back to previous version
- Notes:
  - Any file that is not versioned prior to enabling versioning will have version “null”
  - Suspending versioning does not delete the previous versions

### S3 Encryption for Objects [*]
- There are 4 methods of encrypting objects in S3
  - SSE-S3: encrypts S3 objects using keys handled & managed by AWS
  - SSE-KMS: leverage AWS Key Management Service to manage encryption keys
  - SSE-C: when you want to manage your own encryption keys
  - Client Side Encryption

- It’s important to understand which ones are adapted to which situation
for the exam

### SSE-S3
- SSE-S3: encryption using keys handled & managed by Amazon S3
- Object is encrypted server side
- AES-256 encryption type
- Must set header: ***“x-amz-server-side-encryption": "AES256"***

### SSE-KMS
- SSE-KMS: encryption using keys handled & managed by KMS
- KMS Advantages: user control + audit trail
- Object is encrypted server side
- Must set header: **“x-amz-server-side-encryption": ”aws:kms"**

### SSE-C
- SSE-C: server-side encryption using data keys fully managed by the customer outside of AWS
- Amazon S3 does not store the encryption key you provide
- **HTTPS must be used**
- Encryption key must provided in HTTP headers, for every HTTP request made

### Client Side Encryption
- Client library such as the Amazon S3 Encryption Client
- Clients must encrypt data themselves before sending to S3
- Clients must decrypt data themselves when retrieving from S3
- Customer fully manages the keys and encryption cycle'

### Encryption in transit (SSL/TLS)
- Amazon S3 exposes:
  - HTTP endpoint: non encrypted
  - HTTPS endpoint: encryption in flight

- You’re free to use the endpoint you want, but HTTPS is recommended
- Most clients would use the HTTPS endpoint by default

- HTTPS is mandatory for SSE-C
- Encryption in flight is also called SSL / TLS

## S3 Security
- **User based**
  - IAM policies - which API calls should be allowed for a specific user from IAM
console
- **Resource Based**
  - Bucket Policies - bucket wide rules from the S3 console - allows cross account
  - Object Access Control List (ACL) – finer grain
  - Bucket Access Control List (ACL) – less common
- **Note**: an IAM principal can access an S3 object if
- the user IAM permissions allow it __OR__ the resource policy ALLOWS it
- __AND__ there’s no explicit DENY

### S3 Bucket Policies
- JSON based policies
  - Resources: buckets and objects
  - Actions: Set of API to Allow or Deny
  - Effect: Allow / Deny
  - Principal: The account or user to apply the policy to

- Use S3 bucket for policy to:
  - Grant public access to the bucket
  - Force objects to be encrypted at upload - Grant access to another account (Cross Account)

## Bucket settings for Block Public Access
- Block public access to buckets and objects granted through
  - new access control lists (ACLs)
  - any access control lists (ACLs)
  - new public bucket or access point policies
- Block public and cross-account access to buckets and objects
through any public bucket or access point policies

- **These settings were created to prevent company data leaks**
- If you know your bucket should never be public, leave these on
- Can be set at the account level

### S3 Security - Other
- Networking:
  - Supports VPC Endpoints (for instances in VPC without www internet)
- Logging and Audit:
  - S3 Access Logs can be stored in other S3 bucket
  - API calls can be logged in AWS CloudTrail
- User Security:
  - MFA Delete: MFA (multi factor authentication) can be required in versioned
  buckets to delete objects
  - Pre-Signed URLs: URLs that are valid only for a limited time (ex: premium video service for logged in users)

### S3 Websites
- S3 can host static websites and have them accessible on the www
- The website URL will be:
  - <bucket-name>.s3-website-<AWS-region>.amazonaws.com
  OR
  - <bucket-name>.s3-website.<AWS-region>.amazonaws.com

- If you get a 403 (Forbidden) error, make sure the bucket policy allows
public reads!

### CORS - Explained
- An **origin** is a scheme (protocol), host (domain) and port
  - E.g.: https://www.example.com (implied port is 443 for HTTPS, 80 for HTTP)
- CORS means Cross-Origin Resource Sharing
- ***Web Browser*** based mechanism to allow requests to other origins while
visiting the main origin
- Same origin: http://example.com/app1 & http://example.com/app2
- Different origins: http://www.example.com & http://other.example.com
- The requests won’t be fulfilled unless the other origin allows for the
requests, using **CORS Headers (ex: Access-Control-Allow-Origin)**

Access-Control-Allow-Origin: https://www.example.com
Access-Control-Allow-Methods: GET, PUT, DELETE
CORS – Diagram

### S3 CORS
- If a client does a cross-origin request on our S3 bucket, we need to
enable the correct CORS headers
- **It’s a popular exam question** [*]
- You can allow for a specific origin or for * (all origins)

### Amazon S3 - Consistency Model
- **Read after write consistency for PUTS of new objects**
  - As soon as a new object is written, we can retrieve it
    ex: (PUT 200 => GET 200)
  - This is true, except if we did a GET before to see if the object existed
    ex: (GET 404 => PUT 200 => GET 404) – eventually consistent
- **Eventual Consistency for DELETES and PUTS of existing objects**
  - If we read an object after updating, we might get the older version
    ex: (PUT 200 => PUT 200 => GET 200 (might be older version))
  - If we delete an object, we might still be able to retrieve it for a short time
    ex: (DELETE 200 => GET 200)

- Note: there’s no way to request “strong consistency”

-----

Question 1:
You're trying to upload a 25 GB file on S3 and it's not working
A: X

Question 2:
I tried creating an S3 bucket named "dev" but it didn't work. This is a new AWS Account and I have no buckets at all. What is the cause?
A: Bucket names must be globally unique and "dev" is already taken

Question 3:
You've added files in your bucket and then enabled versioning. The files you've already added will have which version?
A: null

Question 4:
Your client wants to make sure the encryption is happening in S3, but wants to fully manage the encryption keys and never store them in AWS. You recommend
A: X SSE-C

Question 5:
Your company wants data to be encrypted in S3, and maintain control of the rotation policy for the encryption keys, but not know the encryption keys values. You recommend
A: SSE-KMS

  With SSE-KMS you let AWS manage the encryption keys but you have full control of the key rotation policy

Question 6:
Your company does not trust S3 for encryption and wants it to happen on the application. You recommend
A: With Client Side Encryption you perform the encryption yourself and send the encrypted data to AWS directly. AWS does not know your encryption keys and cannot decrypt your data.

Question 7:
The bucket policy allows our users to read/write files in the bucket, yet we were not able to perform a PutObject API call.
A: The IAM user must have an explicit DENY in the attached IAM policy

  Explicit DENY in an IAM policy will take precedence over a bucket policy permission

Question 8:
You have a website that loads files from another S3 bucket. When you try the URL of the files directly in your Chrome browser it works, but when the website you're visiting tries to load these files it doesn't. What's the problem?
A: CORS is wrong

  Cross-origin resource sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. To learn more about CORS, go here: https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html

------

Developing on AWS

## Section Introduction
- So far, we’ve interacts with services manually and they exposed standard
information for clients:
- EC2 exposes a standard Linux machine we can use any way we want
- RDS exposes a standard database we can connect to using a URL
- ElastiCache exposes a cache URL we can connect to using a URL
- ASG / ELB are automated and we don’t have to program against them
- Route53 was setup manual
- Developing against AWS has two components:
- How to perform interactions with AWS without using the Online Console?
- How to interact with AWS Proprietary services? (S3, DynamoDB, etc…)

## Section Introduction
- Developing and performing AWS tasks against AWS can be done in
several ways
- Using the AWS CLI on our local computer
- Using the AWS CLI on our EC2 machines
- Using the AWS SDK on our local computer
- Using the AWS SDK on our EC2 machines
- Using the AWS Instance Metadata Service for EC2
- In this section, we’ll learn:
- How to do all of those
- In the right & most secure way, adhering to best practices

AWS NETWORK
### AWS CLI Configuration
- Let’s learn how to properly configure the CLI
- We’ll learn how to get our access credentials and protect them
- Do not share your AWS Access Key and Secret key with anyone!

### AWS CLI ON EC2… THE BAD WAY
- We could run `aws configure` on EC2 just like we did (and it’ll work)
- But… it’s SUPER INSECURE
- **NEVER EVER EVER PUT YOUR PERSONAL CREDENTIALS ON AN EC2**
- Your **PERSONAL** credentials are **PERSONAL** and only belong on your **PERSONAL** computer

- If the EC2 is compromised, so is your personal account
- If the EC2 is shared, other people may perform AWS actions while impersonating you

- For EC2, there’s a better way… it’s called AWS IAM Roles

### AWS CLI ON EC2… THE RIGHT WAY
- **IAM Roles can be attached to EC2 instances**
- IAM Roles can come with a policy authorizing exactly what the EC2 instance should be able to do
- EC2 Instances can then use these profiles automatically without any additional configurations
- **This is the best practice on AWS and you should 100% do this.**

### AWS EC2 Instance Metadata
- AWS EC2 Instance Metadata is powerful but one of the least known features to developers
- It allows AWS EC2 instances to ”learn about themselves” **without using an IAM Role for that purpose**.
- The URL is http://169.254.169.254/latest/meta-data
- You can retrieve the IAM Role name from the metadata, but you CANNOT
retrieve the IAM Policy.
- Metadata = Info about the EC2 instance
- Userdata = launch script of the EC2 instance

### AWS SDK Overview
- What if you want to perform actions on AWS directly from your applications
code ? (without using the CLI).
- You can use an SDK (software development kit) !
- Official SDKs are…
  - Java
  - .NET
  - Node.js
  - PHP
  - Python (named boto3 / botocore)
  - Go
  - Ruby
  - C++

### AWS SDK Overview
- We have to use the AWS SDK when coding against AWS Services such as DynamoDB

- Fun fact… the AWS CLI uses the Python SDK (boto3)
- The exam expects you to know when you should use an SDK
- We’ll practice the AWS SDK when we get to the Lambda functions

- Good to know: if you don’t specify or configure a default region, then us-east-1 will be chosen by default

### AWS SDK Credentials Security
- It’s recommend to use the **default credential provider chain**
- The **default credential provider chain** works seamlessly with:
  - AWS credentials at ~/.aws/credentials (only on our computers or on premise)
  - Instance Profile Credentials using IAM Roles (for EC2 machines, etc…)
  - Environment variables (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY)

- **Overall, NEVER EVER STORE AWS CREDENTIALS IN YOUR CODE.**
- **Best practice is for credentials to be inherited from mechanisms above, and 100% IAM Roles if working from within AWS Services**

### Exponential Backoff
- Any API that fails because of too many calls needs to be retried with Exponential Backoff
- These apply to rate limited API
- Retry mechanism included in SDK API calls


-----
Question 1:
My EC2 Instance does not have the permissions to perform an API call PutObject on S3. What should I do?
A:

  IAM roles are the right way to provide credentials and permissions to an EC2 instance

Question 2:
I have an on-premise personal server that I'd like to use to perform AWS API calls
  A: O I should run `aws configure` and put my credentials there. Invalidate them when I'm done

    Even better would be to create a user specifically for that one on-premise server

  A: X I should attach an EC2 IAM Role to my personal server

    you can't attach EC2 IAM roles to on premise servers

Question 3:
I need my colleagues help to debug my code. When he runs the application on his machine, it's working fine, whereas I get API authorisation exceptions. What should I do?
A: Compare his IAM policy and my IAM policy in the policy simulator to understand the differences

Question 4:
To get the instance id of my EC2 machine from the EC2 machine, the best thing is to...
A: Query the meta data at http://169.254.169.254/latest/meta-data

-----

Advanced S3
www.datacumulus.com
S3, Glacier, Athena

S3 MFA-Delete
- MFA (multi factor authentication) forces user to generate a code on a device (usually a
mobile phone or hardware) before doing important operations on S3
- To use MFA-Delete, enable Versioning on the S3 bucket
- You will need MFA to
- permanently delete an object version
- suspend versioning on the bucket
- You won’t need MFA for
- enabling versioning
- listing deleted versions
- Only the bucket owner (root account) can enable/disable MFA-Delete
- MFA-Delete currently can only be enabled using the CLI

S3 Default Encryption vs Bucket Policies
- The old way to enable default encryption was to use a bucket policy
and refuse any HTTP command without the proper headers:
- The new way is to use the “default encryption” option in S3
- Note: Bucket Policies are evaluated before “default encryption”

S3 Access Logs
- For audit purpose, you may want to log all access to S3
buckets
- Any request made to S3, from any account, authorized or
denied, will be logged into another S3 bucket
- That data can be analyzed using data analysis tools…
- Or Amazon Athena as we’ll see later in this section!
- The log format is at:
https://docs.aws.amazon.com/AmazonS3/latest/dev/LogFo
rmat.html
My-bucket
Logging Bucket
requests
Log all
requests

S3 Access Logs: Warning
- Do not set your logging bucket to be the monitored bucket
- It will create a logging loop, and your bucket will grow in size exponentially
App Bucket &
Logging Bucket
Logging loop
PutObject
Do not try this at home J

### S3 Replication (CRR & SRR)
- Must enable versioning in source and destination
- Cross Region Replication (CRR)
- Same Region Replication (SRR)
- Buckets can be in different accounts
- Copying is asynchronous
- Must give proper IAM permissions to S3

- __CRR - Use cases__: compliance, lower latency access, replication across accounts
- __SRR - Use cases__: log aggregation, live replication between production and test accounts


### S3 Replication – Notes
- After activating, only new objects are replicated (not retroactive)
- For DELETE operations:
- If you delete without a version ID, it adds a delete marker, not replicated
- If you delete with a version ID, it deletes in the source, not replicated
- There is no “chaining” of replication
- If bucket 1 has replication into bucket 2, which has replication into bucket 3
- Then objects created in bucket 1 are not replicated to bucket 3


### S3 Pre-Signed URLs
- Can generate pre-signed URLs using SDK or CLI
- For downloads (easy, can use the CLI)
- For uploads (harder, must use the SDK)
- Valid for a default of 3600 seconds, can change timeout with --expires-in
[TIME_BY_SECONDS] argument
- Users given a pre-signed URL inherit the permissions of the person who generated the URL for GET / PUT
- Examples :
- Allow only logged-in users to download a premium video on your S3 bucket
- Allow an ever changing list of users to download files by generating URLs dynamically
- Allow temporarily a user to upload a file to a precise location in our bucket

aws --profile pablo-developer s3 presign s3://my-sample-bucket-monitored-pablo/beach.jpg --expires-in 300 --region ap-southeast-2
https://my-sample-bucket-monitored-pablo.s3.ap-southeast-2.amazonaws.com/beach.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAYZ33DWH4ML6QNG3%2F20200527%2Fap-southeast-2%2Fs3%2Faws4_request&X-Amz-Date=20200527T035233Z&X-Amz-Expires=300&X-Amz-SignedHeaders=host&X-Amz-Signature=d3574302ba10d7197de6b58cf605a1b73c49e3ccf064410acb1c251c42fbe38e

### S3 Storage Classes [*]
- Amazon S3 Standard - General Purpose
- Amazon S3 Standard-Infrequent Access (IA)
- Amazon S3 One Zone-Infrequent Access
- Amazon S3 Intelligent Tiering
- Amazon Glacier
- Amazon Glacier Deep Archive

- Amazon S3 Reduced Redundancy Storage (deprecated - omitted)

### S3 Standard – General Purpose
- High durability (99.999999999%) of objects across multiple AZ
- If you store 10,000,000 objects with Amazon S3, you can on average
expect to incur a loss of a single object once every 10,000 years
- 99.99% Availability over a given year
- Sustain 2 concurrent facility failures

- **Use Cases**: **Big Data analytics, mobile & gaming applications, content distribution…**

### S3 Standard – Infrequent Access (IA)
- Suitable for data that is less frequently accessed, but requires rapid
access when needed
- High durability (99.999999999%) of objects across multiple AZs
- 99.9% Availability
- Low cost compared to Amazon S3 Standard
- Sustain 2 concurrent facility failures

- **Use Cases**: **As a data store for disaster recovery, backups…**

S3 One Zone - Infrequent Access (IA)
- Same as IA but data is stored in a single AZ
- High durability (99.999999999%) of objects in a single AZ; data lost when AZ
is destroyed
- 99.5% Availability
- Low latency and high throughput performance
- Supports SSL for data at transit and encryption at rest
- Low cost compared to IA (by 20%)

- **Use Cases: Storing secondary backup copies of on-premise data, or storing
data you can recreate**

### S3 Intelligent Tiering
- Same low latency and high throughput performance of S3 Standard
- Small monthly monitoring and auto-tiering fee
- Automatically moves objects between two access tiers based on
changing access patterns
- Designed for durability of 99.999999999% of objects across multiple
Availability Zones
- Resilient against events that impact an entire Availability Zone
- Designed for 99.9% availability over a given year

### Amazon Glacier
- Low cost object storage meant for archiving / backup
- Data is retained for the longer term (10s of years)
- Alternative to on-premise magnetic tape storage
- Average annual durability is 99.999999999%
- Cost per storage per month ($0.004 / GB) + retrieval cost
- Each item in Glacier is called “**Archive”** (up to 40TB)
- Archives are stored in ”**Vaults**”

### Amazon Glacier & Glacier Deep Archive [*]
- Amazon Glacier – 3 retrieval options:
  - Expedited (1 to 5 minutes)
  - Standard (3 to 5 hours)
  - Bulk (5 to 12 hours)
  - Minimum storage duration of 90 days

- Amazon Glacier Deep Archive – for long term storage – cheaper:
  - Standard (12 hours)
  - Bulk (48 hours)
  - Minimum storage duration of 180 days

### S3 Storage Classes Comparison
https://aws.amazon.com/s3/storage-classes/

[SAAC-02]
### S3 – Moving between storage classes
- You can transition objects between storage classes
- For infrequently accessed object, move them to STANDARD_IA
- For archive objects you don’t need in real
-time, GLACIER or DEEP_ARCHIVE
- Moving objects can be automated using a lifecycle configuration

### S3 Lifecycle Rules
- **Transition actions**: It defines when objects are transitioned to another storage class.
  - Move objects to Standard IA class 60 days after creation
  - Move to Glacier for archiving after 6 months

- Expiration actions: configure objects to expire (delete) after some time
  - Access log files can be set to delete after a 365 days
  - **Can be used to delete old versions of files (if versioning is enabled)**
  - Can be used to delete incomplete multi-part uploads

- Rules can be created for a certain prefix (ex - s3://mybucket/mp3/*)
- Rules can be created for certain objects tags (ex - Department: Finance)

### S3 Lifecycle Rules – Scenario 1
- **Your application on EC2 creates images thumbnails after profile photos are uploaded to Amazon S3. These thumbnails can be easily recreated, and only need to be kept for 45 days. The source images should be able to be immediately retrieved for these 45 days, and afterwards, the user can wait up to 6 hours. How would you design this?**

- S3 source images can be on STANDARD, with a lifecycle configuration
to transition them to GLACIER after 45 days.
- S3 thumbnails can be on ONEZONE_IA, with a lifecycle configuration
to expire them (delete them) after 45 days.

### S3 Lifecycle Rules – Scenario 2
- **A rule in your company states that you should be able to recover your deleted S3 objects immediately for 15 days, although this may happen rarely. After this time, and for up to 365 days, deleted objects should be recoverable within 48 hours.**
- You need to enable S3 versioning in order to have object versions, so that
“deleted objects” are in fact hidden by a “delete marker” and can be
recovered

- You can transition these “noncurrent versions” of the object to S3_IA
- You can transition afterwards these “noncurrent versions” to
DEEP_ARCHIVE

[SAAC-02]
### S3 – Baseline Performance
- Amazon S3 automatically scales to high request rates, latency 100-200 ms
- Your application can achieve at least **3,500 PUT/COPY/POST/DELETE and 5,500 GET/HEAD requests per second per prefix in a bucket.**
- There are no limits to the number of prefixes in a bucket.
- __Example (object path => prefix)__:
  - bucket/folder1/sub1/file => /folder1/sub1/
  - bucket/folder1/sub2/file => /folder1/sub2/
  - bucket/1/file => /1/
  - bucket/2/file => /2/
- If you spread reads across all four prefixes evenly, you can achieve 22,000
requests per second for GET and HEAD

### S3 – KMS Limitation
- If you use SSE-KMS, you may be impacted by the KMS limits
- When you upload, it calls the **GenerateDataKey** KMS API
- When you download, it calls the **Decrypt** KMS API
- Count towards the KMS quota per second (5500, 10000, 30000 req/s based on region)
- As of today, you cannot request a quota increase for KMS

### S3 Performance
- **Multi-Part upload**:
  - recommended for files > 100MB, must use for files > 5GB
  - Can help parallelize uploads (speed up transfers)

- **S3 Transfer Acceleration (upload only)**
  - Increase transfer speed by transferring file to an AWS edge location which will
  forward the data to the S3 bucket in the target region
  - Compatible with multi-part upload

### S3 Performance – S3 Byte-Range Fetches
- **Parallelize GETs by requesting** specific byte ranges
- Better resilience in case of failures

- __Can be used to speed up downloads__
- __Can be used to retrieve only partial data (for example the head of a file)__

### S3 Select & Glacier Select
- Retrieve less data using SQL by performing **server side filtering**
- Can filter by rows & columns (simple SQL statements)
- Less network transfer, less CPU cost client-side

https://aws.amazon.com/blogs/aws/s3-glacier-select/

---

### S3 Event Notifications
Amazon S3
- S3:ObjectCreated, S3:ObjectRemoved,
  S3:ObjectRestore, S3:Replication…
- Object name filtering possible (*.jpg)
- __Use case__: generate thumbnails of images uploaded to S3
- **Can create as many “S3 events” as desired**

- S3 event notifications typically deliver events in seconds but can sometimes take a minute or longer
- If two writes are made to a single non-versioned object at the same time, it is possible that only a single event notification will be sent
- If you want to ensure that an event notification is sent for every successful write, you can enable versioning on your bucket.

### AWS Athena
- **Serverless** service to perform analytics **directly against S3 files**
- Uses SQL language to query the files
- Has a JDBC / ODBC driver
- Charged per query and amount of data scanned
- Supports CSV, JSON, ORC, Avro, and Parquet (built on Presto)
- Use cases: Business intelligence / analytics / reporting, analyze & query
VPC Flow Logs, ELB Logs, CloudTrail trails, etc...
- Exam Tip: Analyze data directly on S3 => use Athena

### S3 Object Lock & Glacier Vault Lock
- **S3 Object Lock**
  - Adopt a WORM (Write Once Read Many) model
  - Block an object version deletion for a specified amount of time

- **Glacier Vault Lock**
  - Adopt a WORM (Write Once Read Many) model
  - Lock the policy for future edits (can no longer be changed)
  - Helpful for compliance and data retention

-----
S3 Advanced & Athena - Quiz

Question 1:
You have enabled versioning and want to be extra careful when it comes to deleting files on S3. What should you enable to prevent accidental permanent deletions?
A: Enable MFA Delete

  MFA Delete forces users to use MFA tokens before deleting objects. It's an extra level of security to prevent accidental deletes

Question 2:
You would like all your files in S3 to be encrypted by default. What is the optimal way of achieving this?
A: Enable "Default Encryption" on S3

Question 3:
You suspect some of your employees to try to access files in S3 that they don't have access to. How can you verify this is indeed the case without them noticing?
A: Enable S3 Access logs analyze the using Athena

  S3 Access Logs log all the requests made to buckets, and Athena can then be used to run serverless analytics on top of the logs files

Question 4:
You are looking for your entire S3 bucket to be available fully in a different region so you can perform data analysis optimally at the lowest possible cost. Which feature should you use?
A: S3  Cross Region Replication CRR

  S3 CRR is used to replicate data from an S3 bucket to another one in a different region

Question 5:
You are looking to provide temporary URLs to a growing list of federated users in order to allow them to perform a file upload on S3 to a specific location. What should you use?
A: S3 Pre-Signer URK

  Pre-Signed URL are temporary and grant time-limited access to some actions in your S3 bucket.

Question 6:
How can you automate the transition of S3 objects between their different tiers?
A: Use S3 Lifecycle Rules

Question 7:
Which of the following is NOT a Glacier retrieval mode?
A: Instan (10 seconds)

Question 8:
Which of the following is a Serverless data analysis service allowing you to query data in S3?
A: Athena

Question 9:
[SAA-C02] You are looking to build an index of your files in S3, using Amazon RDS PostgreSQL. To build this index, it is necessary to read the first 250 bytes of each object in S3, which contains some metadata about the content of the file itself. There is over 100,000 files in your S3 bucket, amounting to 50TB of data. how can you build this index efficiently?
A: Create an application that will traverse the S3 bucket, issue a Byte Range Fetch for the first 250 bytes, and store that information in RDS.

-----

## AWS CloudFront
- Content Delivery Network (CDN)
- Improves read performance, content is cached at the edge
- 216 Point of Presence globally (edge locations)
- DDoS protection, integration with Shield, AWS Web Application Firewall
- Can expose external HTTPS and can talk to internal HTTPS backends

https://aws.amazon.com/cloudfront/features/?nc=sn&loc=2

### CloudFront – Origins
- ***S3 bucket***
  - For distributing files and caching them at the edge
  - Enhanced security with CloudFront ***Origin Access Identity (OAI)***
  - CloudFront can be used as an ingress (to upload files to S3)

- **Custom Origin (HTTP)**
  - Application Load Balancer
  - EC2 instance
  - S3 website (must first enable the bucket as a static S3 website)
  - Any HTTP backend you want

### CloudFront Geo Restriction
- You can restrict who can access your distribution
  - **Whitelist**: Allow your users to access your content only if they're in one of the countries on a list of approved countries.
  - **Blacklist**: Prevent your users from accessing your content if they're in one of the countries on a blacklist of banned countries.

- The “country” is determined using a 3rd party Geo-IP database
- Use case: Copyright Laws to control access to content

### CloudFront vs S3 Cross Region Replication
- CloudFront:
  - Global Edge network
  - Files are cached for a TTL (maybe a day)
  - **Great for static content that must be available everywhere**

- S3 Cross Region Replication:
  - Must be setup for each region you want replication to happen
  - Files are updated in near real-time
  - Read only
  - **Great for dynamic content that needs to be available at low-latency in few regions**

### AWS CloudFront Hands On
- We’ll create an S3 bucket
- We’ll create a CloudFront distribution
- We’ll create an Origin Access Identity
- We’ll limit the S3 bucket to be accessed only using this identity

[SAA-C02]
### CloudFront Signed URL / Signed Cookies
- You want to distribute paid shared content to premium users over the world
- We can use CloudFront Signed URL / Cookie. We attach a policy with:
  - Includes URL expiration
  - Includes IP ranges to access the data from
  - Trusted signers (which AWS accounts can create signed URLs)
- How long should the URL be valid for?
  - Shared content (movie, music): make it short (a few minutes)
  - Private content (private to the user): you can make it last for years

- Signed URL = access to individual files (one signed URL per file)
- Signed Cookies = access to multiple files (one signed cookie for many files)

[SAA-C02]
### CloudFront Signed URL vs S3 Pre-Signed URL
- CloudFront Signed URL:
  - Allow access to a path, no matter the origin
  - Account wide key-pair, only the root can manage it
  - Can filter by IP, path, date, expiration
  - Can leverage caching features

- S3 Pre-Signed URL:
  - Issue a request as the person who pre-signed the URL
  - Uses the IAM key of the signing IAM principal
  - Limited lifetime


https://aws.amazon.com/global-accelerator/pricing/


-----
CloudFront & AWS Global Accelerator Quiz

Question 1:
Which features allows us to distribute paid content from S3 securely, globally, if the S3 bucket is secured to only exchange data with CloudFront?
A: CloudFront Signed URL

  CloudFront Signed URL are commonly used to distribute paid content through dynamic CloudFront Signed URL generation.

Question 2:
You are hosting highly dynamic content in Amazon S3 in us-east-1. Recently, there has been a need to make that data available with low latency in Singapore. What do you recommend using?
A: S3 Cross Region Replication

  S3 CRR allows you to replicate the data from one bucket in a region to another bucket in another region

Question 3:
How can you ensure that only users who access our website through Canada are authorized in CloudFront?
A: Use CloudFront Geo Restriction

Question 4:
You would like to provide your users access to hundreds of private files in your CloudFront distribution, which is fronting an HTTP web server behind an application load balancer. What should you use?
A: CloudFront Signed Cookies

  Allows you to access many files

Question 5:
[SAA-C02] You are creating an application that is going to expose an HTTP REST API. There is a need to provide request routing rules at the HTTP level. Due to security requirements, your application can only be exposed through the use of two static IPs. How can you create a solution that validates these requirements?
A: Use Global Accelerator and an Application Load Balancer.

  Global Accelerator will provide us with the two static IP, and the ALB will provide use with the HTTP routing rules


What does this S3 bucket policy do?

 {
   "Version":"2012-10-17",
   "Id":"Mystery policy",
   "Statement":[
     {
       "Sid":"What could it be?",
       "Effect":"Allow",
       "Principal":{"CanonicalUser":"CloudFront Origin Identity Canonical User ID"},
       "Action":"s3:GetObject",
       "Resource":"arn:aws:s3:::examplebucket/*"
     }
   ]
}

A: Only allows the S3 bucket content to be accessed from your CloudFront distribution origin identity

-----

Section 13: AWS Storage Extras

### AWS Storage Gateway Summary
- Exam tip: Read the question well, it will hint at which gateway to use
- On premise data to the cloud => Storage Gateway

- File access / NFS => File Gateway
(backed by S3)
- Volumes / Block Storage / iSCSI => Volume gateway
(backed by S3 with EBS snapshots)
- VTL Tape solution / Backup with iSCSI = > Tape Gateway
(backed by S3 and Glacier)

### Amazon FSx for Windows (File Server)
- EFS is a shared POSIX system for Linux systems.

- **FSx for Windows** is a fully managed **Windows** file system share drive
- Supports SMB protocol & Windows NTFS
- Microsoft Active Directory integration, ACLs, user quotas
- Built on SSD, scale up to 10s of GB/s, millions of IOPS, 100s PB of data
- Can be accessed from your on-premise infrastructure
- Can be configured to be Multi-AZ (high availability)
- Data is backed-up daily to S3

### Amazon FSx for Lustre
- Lustre is a type of parallel distributed file system, for large-scale computing
- The name Lustre is derived from “Linux” and “cluster”

- Machine Learning, **High Performance Computing (HPC)**
- Video Processing, Financial Modeling, Electronic Design Automation
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- **Seamless integration with S3**
  - Can “read S3” as a file system (through FSx)
  - Can write the output of the computations back to S3 (through FSx)
- Can be used from on-premise servers

### Storage Comparison
- S3: Object Storage
- Glacier: Object Archival
- EFS: Network File System for Linux instances, POSIX filesystem
- FSx for Windows: Network File System for Windows servers
- FSx for Lustre: High Performance Computing Linux file system
- EBS volumes: Network storage for one EC2 instance at a time
- Instance Storage: Physical storage for your EC2 instance (high IOPS)
- Storage Gateway: File Gateway, Volume Gateway (cache & stored), Tape Gateway
- Snowball / Snowmobile: to move large amount of data to the cloud, physically
- Database: for specific workloads, usually with indexing and querying

----
### AWS Storage Extras - Quiz

Question 1:
You need to move hundreds of Terabytes into the cloud in S3, and after that pre-process it using many EC2 instances in order to clean the data. You have a 1 Gbit/s broadband and would like to optimize the process of moving the data and pre-processing it, in order to save time. What do you recommend?
A: Use Snowball Edge

  Snowball Edge is the right answer as it comes with computing capabilities and allows use to pre-process the data while it's being moved in Snowball, so we save time on the pre-processing side as well.

Question 2:
You want to expose a virtually infinite storage for your tape backups. You want to keep the same software as today and want a iSCSI compatible interface. What do you use?
A: Tape Gateway

Question 3:
Your EC2 Windows Servers need to share some data by having a Network File System mounted, that respect the Windows security mechanisms and has integration with Active Directory. What do you recommend putting in place as an NFS?
A: FSx for Windows


Question 4:
You would like to have a distributed POSIX compliant file system that will allow you to maximize the IOPS in order to perform some HPC and genomics computational research. That file system will have to scale easily to millions of IOPS. What do you recommend?
A: FSx for Lustre

----

# Section 14: Decoupling applications: SQS, SNS, Kinesis, Active MQ


## Section Introduction
- Synchronous between applications can be problematic if there are sudden spikes of traffic
- What if you need to suddenly encode 1000 videos but usually it’s 10?

- In that case, it’s better to **decouple** your applications,
  - using SQS: queue model
  - using SNS: pub/sub model
  - using Kinesis: real-time streaming model
- These services can scale independently from our application!


### AWS SQS – Standard Queue
- Oldest offering (over 10 years old)
- Fully managed
- Scales from 1 message per second to 10,000s per second
- Default retention of messages: 4 days, maximum of 14 days
- No limit to how many messages can be in the queue
- Low latency (<10 ms on publish and receive)
- Horizontal scaling in terms of number of consumers
- Can have duplicate messages (at least once delivery, occasionally)
- Can have out of order messages (best effort ordering)
- Limitation of 256KB per message sent

### AWS SQS – Delay Queue
- Delay a message (consumers don’t see it immediately) up to **15 minutes**
- Default is 0 seconds (message is available right away)
- Can set a default at queue level
- Can override the default using the **DelaySeconds** parameter

### SQS – Consuming Messages
- Consumers…
- Poll SQS for messages (receive up to 10 messages at a time)
- Process the message within the visibility timeout
- Delete the message using the message ID & receipt handle

### SQS –Visibility timeout
- When a consumer polls a message from a queue, the message is “invisible” to other
consumers for a defined period… the **Visibility Timeout**:
  - Set between 0 seconds and 12 hours (default 30 seconds)
  - If too high (15 minutes) and consumer fails to process the message,  you must wait a long time before processing the message again
  - If too low (30 seconds) and consumer needs time to process the message (2 minutes), another
consumer will receive the message and the message will be processed more than once
- **ChangeMessageVisibility** API to change the visibility while processing a message
- **DeleteMessage** API to tell SQS the message was successfully processed

### AWS SQS – Dead Letter Queue
- If a consumer fails to process a message within the Visibility Timeout…
  the message goes back to the queue!
- We can set a threshold of how many times a message can go back to the queue – it’s
called a “redrive policy”
- After the threshold is exceeded, the message goes into a dead letter queue (DLQ)
- We have to create a DLQ first and then designate it dead letter queue
- Make sure to process the messages in the DLQ before they expire!

### AWS SQS - Long Polling
- When a consumer requests message from the queue, it can optionally “wait” for messages to arrive if there are none in the queue
- This is called Long Polling
- **LongPolling decreases the number of API calls made to SQS while increasing the efficiency and latency of your application.**
- The wait time can be between 1 sec to 20 sec (20 sec preferable)
- Long Polling is preferable to Short Polling
- Long polling can be enabled at the queue level or at the API level using **WaitTimeSeconds**

### AWS SQS – FIFO Queue
- Newer offering (First In - First out) – not available in all regions!
- Name of the queue must end in .fifo - Lower throughput (up to 3,000 per second  with batching, 300/s without)
- Messages are processed in order by the consumer
- Messages are sent exactly once
- No per message delay (only per queue delay)
- Ability to do content based  de-duplication
- 5-minute interval de-duplication using “Duplication ID”
- Message Groups:
  - Possibility to group messages for FIFO ordering using “Message GroupID”
  - Only one worker can be assigned per message group so that messages are processed in order
  - Message group is just an extra tag on the message!


### AWS SNS
- The “event producer” only sends message to one SNS topic
- As many “event receivers” (subscriptions) as we want to listen to the SNS topic notifications
- Each subscriber to the topic will get all the messages (note: new feature to filter messages)
- Up to 10,000,000 subscriptions per topic
- 100,000 topics limit
- Subscribers can be:
  - SQS
  - HTTP / HTTPS (with delivery retries – how many times)
  - Lambda
  - Emails
  - SMS messages
  - Mobile Notifications

### SNS integrates with a lot of Amazon Products
- Some services can send data directly to SNS for notifications
- CloudWatch (for alarms)
- Auto Scaling Groups notifications
- Amazon S3 (on bucket events)
- CloudFormation (upon state changes => failed to build, etc)
- Etc…

### AWS SNS – How to publish
- Topic Publish (within your AWS Server – using the SDK)
  - Create a topic
  - Create a subscription (or many)
  - Publish to the topic

- Direct Publish (for mobile apps SDK)
  - Create a platform application
  - Create a platform endpoint
  - Publish to the platform endpoint
  - Works with Google GCM, Apple APNS, Amazon ADM…

### SNS + SQS: Fan Out Pattern
- Push once in SNS, receive in many SQS
- Fully decoupled
- No data loss
- Ability to add receivers of data later
- SQS allows for delayed processing
- SQS allows for retries of work
- May have many workers on one queue and one worker on the other queue

### AWS Kinesis Overview
- Kinesis is a managed alternative to Apache Kafka.
- Great for application logs, metrics, IoT, clickstreams
- **Great for “real-time” big data**
- Great for streaming processing frameworks (Spark, NiFi, etc…)
- Data is automatically replicated to 3 AZ

- **Kinesis Streams**: low latency streaming ingest at scale
- **Kinesis Analytics**: perform real-time analytics on streams using SQL
- **Kinesis Firehose**: load streams into S3, Redshift, ElasticSearch…

### Kinesis Streams Shards
- One stream is made of many different shards
- 1MB/s or 1000 messages/s at write PER SHARD
- 2MB/s at read PER SHARD
- Billing is per shard provisioned, can have as many shards as you want
- Batching available or per message calls.
- The number of shards can evolve over time (reshard / merge)
- **Records are ordered per shard**

### SQS vs SNS vs Kinesis
**SQS**:
- Consumer “pull data”
- Data is deleted after being consumed
- Can have as many workers (consumers) as we want
- No need to provision throughput
- No ordering guarantee (except FIFO queues)
- Individual message delay capability
**SNS**:
- Push data to many subscribers
- Up to 10,000,000 subscribers
- Data is not persisted (lost if not delivered)
- Pub/Sub
- Up to 100,000 topics
- No need to provision throughput
- Integrates with SQS for fan-out architecture pattern
**Kinesis**:
- Consumers “pull data”
- As many consumers as we want
- Possibility to replay data
- Meant for real-time big data, analytics and ETL
- Ordering at the shard level
- Data expires after X days
- Must provision throughput

## Amazon MQ
- SQS, SNS are “cloud-native” services, and they’re using proprietary protocols from AWS.
- Traditional applications running from on-premise may use open protocols such as: MQTT, AMQP, STOMP, Openwire, WSS
- When migrating to the cloud, instead of re-engineering the application to use SQS and SNS, we can use Amazon MQ
- **Amazon MQ = managed Apache ActiveMQ**

- Amazon MQ doesn’t “scale” as much as SQS / SNS
- Amazon MQ runs on a dedicated machine, can run in HA with failover
- Amazon MQ has both queue feature (~SQS) and topic features (~SNS)

-----
Messaging and Integration Quiz
Quiz 13|12 questions

Question 1:
You are preparing for the biggest day of sale of the year, where your traffic will increase by 100x. You have already setup SQS standard queue. What should you do?
A: Do nothing, SQS scales automatically

Question 2:
You would like messages to be processed by SQS consumers only after 5 minutes of being published to SQS. What should you do?



Question 4:
Your SQS costs are extremely high. Upon closer look, you notice that your consumers are polling SQS too often and getting empty data as a result. What should you do?
A: Enable Long Polling

  Long polling helps reduce the cost of using Amazon SQS by eliminating the number of empty responses (when there are no messages available for a ReceiveMessage request) and false empty responses (when messages are available but aren't included in a response)

Question 5:
You'd like your messages to be processed exactly once and in order. Which do you need?
A: SQS FIFO Queue

  FIFO (First-In-First-Out) queues are designed to enhance messaging between applications when the order of operations and events is critical, or where duplicates can't be tolerated. FIFO queues also provide exactly-once processing but have a limited number of transactions per second (TPS).

Question 6:
You'd like to send a message to 3 different applications all using SQS. You should
A: Use SNS + SQS Fan Out pattern

  This is a common pattern as only one message is sent to SNS and then "fan out" to multiple SQS queuesee

Question 7:
You have a Kinesis stream usually receiving 5MB/s of data and sending out 8 MB/s of data. You have provisioned 6 shards. Some days, your traffic spikes up to 2 times and you get a throughput exception. You should
A: Add more shards

  Each shard allows for 1MB/s incoming and 2MB/s outgoing of data

Question 8:
You are sending a clickstream for your users navigating your website, all the way to Kinesis. It seems that the users data is not ordered in Kinesis, and the data for one individual user is spread across many shards. How to fix that problem?
A: You should use a partition key that represents the identity of the user

  By providing a partition key we ensure the data is ordered for our users

Question 9:
We'd like to perform real time analytics on streams of data. The most appropriate product will be
A: Kinesis

  Kinesis Analytics is the product to use, with Kinesis Streams as the underlying source of data

Question 10:
We'd like for our big data to be loaded near real time to S3 or Redshift. We'd like to convert the data along the way. What should we use?
A: Kinesis Streams + Kinesis Firehose

  This is a perfect combo of technology for loading data near real-time in S3 and Redshift

Question 11:
You want to send email notifications to your users. You should use
A: SNS

  Has that feature by default

Question 12:
You have many microservices running on-premise and they currently communicate using a message broker that supports the MQTT protocol. You would like to migrate these applications and the message broker to the cloud without changing the application logic. Which technology allows you to get a managed message broker that supports the MQTT protocol?
A: Amazon MQ

  Supports JMS, NMS, AMQP, STOMP, MQTT, and WebSocket


-----

## Section 15: Serverless Overviews from a Solution Architect Perspective

What’s serverless?
- Serverless is a new paradigm in which the developers don’t have to manage servers anymore…
- They just deploy code
- They just deploy… functions !
- Initially... **Serverless == FaaS (Function as a Service)**
- Serverless was pioneered by AWS Lambda but now also includes
anything that’s managed: “databases, messaging, storage, etc.”
- **Serverless does not mean there are no servers…**
it means you just don’t manage / provision / see them

### Serverless in AWS
- AWS Lambda
- DynamoDB
- AWS Cognito
- AWS API Gateway
- Amazon S3
- AWS SNS & SQS
- AWS Kinesis Data Firehose
- Aurora Serverless
- Step Functions
- Fargate

### Why AWS Lambda
**Amazon EC2**
- Virtual Servers in the Cloud
- Limited by RAM and CPU
- Continuously running
- Scaling means intervention to add / remove servers
**Amazon Lambda**
- Virtual **functions** – no servers to manage!
- Limited by time - **short executions**
- Run **on-demand**
- **Scaling is automated!**

### Benefits of AWS Lambda
- Easy Pricing:
  - Pay per request and compute time
  - Free tier of 1,000,000 AWS Lambda requests and 400,000 GBs of compute time

- Integrated with the whole AWS suite of services
- Integrated with many programming languages
- Easy monitoring through AWS CloudWatch
- Easy to get more resources per functions (up to 3GB of RAM!)
- **Increasing RAM will also improve CPU and network!**

### AWS Lambda language support
- Node.js (JavaScript)
- Python
- Java (Java 8 compatible)
- C# (.NET Core)
- Golang
- C# / Powershell
- Ruby
- Custom Runtime API (community supported, example Rust)
- Important: Docker is not for AWS Lambda, it’s for ECS / Fargate

AWS Lambda Pricing: example
- You can find overall pricing information here:
  https://aws.amazon.com/lambda/pricing/
- Pay per **calls**:
  - First 1,000,000 requests are free
  - $0.20 per 1 million requests thereafter ($0.0000002 per request)
- Pay per **duration**: (in increment of 100ms)
  - 400,000 GB-seconds of compute time per month if FREE
  - == 400,000 seconds if function is 1GB RAM
  - == 3,200,000 seconds if function is 128 MB RAM
  - After that $1.00 for 600,000 GB-seconds
- It is usually __very cheap__ to run AWS Lambda so it’s __very popular__.

### AWS Lambda Limits to Know - per region
- **Execution:**
  - Memory allocation: 128 MB – 3008 MB (64 MB increments)
  - Maximum execution time: 900 seconds (15 minutes)
  - Environment variables (4 KB)
  - Disk capacity in the “function container” (in /tmp): 512 MB
  - Concurrency executions: 1000 (can be increased)
- **Deployment**:
  - Lambda function deployment size (compressed .zip): 50 MB
  - Size of uncompressed deployment (code + dependencies): 250 MB
  - Can use the /tmp directory to load other files at startup
  - Size of environment variables: 4 KB

### Lambda@Edge
- You have deployed a CDN using CloudFront
- What if you wanted to run a global AWS Lambda alongside?
- Or how to implement request filtering before reaching your application?

- For this, you can use Lambda@Edge:
  deploy Lambda functions alongside your CloudFront CDN
  - Build more responsive applications
  - You don’t manage servers, Lambda is deployed globally
  - Customize the CDN content
  - Pay only for what you use

### Lambda@Edge
- You can use Lambda to change CloudFront requests and responses:
  - After CloudFront receives a request from a viewer (viewer request)
  - Before CloudFront forwards the request to the origin (origin request)
  - After CloudFront receives the response from the origin (origin response)
  - Before CloudFront forwards the response to the viewer (viewer response)

- You can also generate responses to viewers without ever sending the request to the origin.

### Lambda@Edge: Use Cases
- Website Security and Privacy
- Dynamic Web Application at the Edge
- Search Engine Optimization (SEO)
- Intelligently Route Across Origins and Data Centers
- Bot Mitigation at the Edge
- Real-time Image Transformation
- A/B Testing
- User Authentication and Authorization
- User Prioritization
- User Tracking and Analytics

### AWS API Gateway
- AWS Lambda + API Gateway: No infrastructure to manage
- Support for the WebSocket Protocol
- Handle API versioning (v1, v2…)
- Handle different environments (dev, test, prod…)
- Handle security (Authentication and Authorization)
- Create API keys, handle request throttling
- Swagger / Open API import to quickly define APIs
- Transform and validate requests and responses
- Generate SDK and API specifications
- Cache API responses

### API Gateway – Integrations High Level
- **Lambda Function**
  - Invoke Lambda function
  - Easy way to expose REST API backed by AWS Lambda
- **HTTP**
  - Expose HTTP endpoints in the backend
  - Example: internal HTTP API on premise, Application Load Balancer…
  - Why? Add rate limiting, caching, user authentications, API keys, etc…
- **AWS Service**
  - Expose any AWS API through the API Gateway?
  - Example: start an AWS Step Function workflow, post a message to SQS
  - Why? Add authentication, deploy publicly, rate control…

### API Gateway - Endpoint Types
- Edge-Optimized (default): For global clients
  - Requests are routed through the CloudFront Edge locations (improves latency)
  - The API Gateway still lives in only one region
- Regional:
  - For clients within the same region
  - Could manually combine with CloudFront (more control over the caching
    strategies and the distribution)
- Private:
  - Can only be accessed from your VPC using an interface VPC endpoint (ENI)
  - Use a resource policy to define access

## API Gateway – Security
IAM Permissions
- Create an IAM policy authorization and attach to User / Role
- API Gateway verifies IAM permissions passed by the calling application
- Good to provide access within your own infrastructure
- Leverages “**Sig v4**” capability where IAM credential are in headers


### API Gateway – Security
**Lambda Authorizer (formerly Custom Authorizers)**
- Uses AWS Lambda to validate the token in header being passed
- Option to cache result of authentication
- Helps to use OAuth / SAML / 3rd party type of authentication
- Lambda must return an IAM policy for the user

### API Gateway – Security
Cognito User Pools
- Cognito fully manages user lifecycle
- API gateway verifies identity automatically from AWS Cognito
- No custom implementation required
- __Cognito only helps with authentication, not authorization__

## API Gateway – Security – Summary
- **IAM:**
  - Great for users / roles already within your AWS account
  - Handle authentication + authorization
  - Leverages Sig v4
- **Custom Authorizer:**
  - Great for 3rd party tokens
  - Very flexible in terms of what IAM policy is returned
  - Handle Authentication + Authorization
  - Pay per Lambda invocation
- **Cognito User Pool:**
  - You manage your own user pool (can be backed by Facebook, Google login etc…)
  - No need to write any custom code
  - Must implement authorization in the backend

## AWS Cognito – Federated Identity Pools
- Goal:
  - Provide direct access to AWS Resources from the Client Side
- How:
  - Log in to federated identity provider – or remain anonymous
  - Get temporary AWS credentials back from the Federated Identity Pool
  - These credentials come with a pre-defined IAM policy stating their permissions
- Example:
  - provide (temporary) access to write to S3 bucket using Facebook Login

### AWS SAM - Serverless Application Model
- **SAM = Serverless Application Model**
- Framework for developing and deploying serverless applications
- All the configuration is YAML code
  - Lambda Functions
  - DynamoDB tables
  - API Gateway
  - Cognito User Pools
- SAM can help you to run Lambda, API Gateway, DynamoDB locally
- SAM can use **CodeDeploy** to deploy Lambda functions

------
Serverless Quiz

Question 1:
You have a Lambda function that will process data for 25 minutes before successfully completing. The code is working fine in your machine, but in AWS Lambda it just fails with a "timeout" issue after 3 seconds. What should you do?
A: Run your code somewhere else than Lambda - the maximum timeout is 15 minutes

Question 2:
You'd like to have a dynamic DB_URL variable loaded in your Lambda code
A: Place it in the environment variables

Question 3:
We have to provision the instance type for our DynamoDB database
A: False

  DynamoDB is a serverless service and as such we don't provision an instance type for our database. We just say how much RCU and WCU we require for our table (or auto scaling)

Question 4:
A DynamoDB table has been provisioned with 10 RCU and 10 WCU. You would like to increase the RCU to sustain more read traffic. What is true about RCU and WCU?
A: RCU and WCU are decoupled, so WCU can stay the same

Question 5:
You are about to enter the Christmas sale and you know a few items in your website are very popular and will be read often. Last year you had a ProvisionedThroughputExceededException. What should you do this year?
A: Create a DAX cluter

  A DynamoDB Accelerator (DAX) cluster is a cache that fronts your DynamoDB tables and caches the most frequently read values. They help offload the heavy reads on hot keys off of DynamoDB itself, hence preventing the ProvisionedThroughputExceededException

Question 6:
You would like to automate sending welcome emails to the users who subscribe to the Users table in DynamoDB. How can you achieve that?
A: Enable DynamoDB Streams and have the Lambda function receive the events in real-time

Question 7:
To make a serverless API, I should integrate API Gateway with
A: Lambda

Question 8:
You would like to provide a Facebook login before your users call your API hosted by API Gateway. You need seamlessly authentication integration, you will use
a: Conigto User Pools

  Cognito User Pools directly integration with Facebook Logins

Question 9:
[SAA-C02] Your production application is leveraging DynamoDB as its backend and is experiencing smooth sustained usage. There is a need to make the application run in development as well, where it will experience unpredictable, sometimes high, sometimes low volume of requests. You would like to make sure you optimize for cost. What do you recommend?
A: OJO X

  Provision WCU &amp;&nbsp;RCU&nbsp;and enable auto-scaling for production and use on-demand capacity for development

------

## Serverless Architectures


### Mobile application: MyTodoList
- We want to create a mobile application with the following requirements

- Expose as REST API with HTTPS
- Serverless architecture
- Users should be able to directly interact with their own folder in S3
- Users should authenticate through a managed serverless service
- The users can write and read to-dos, but they mostly read them
- The database should scale, and have some high read throughput

[*] Store files on S3 from mobile, use Amazon Cognito to generate temp credentials via AWS STS.

[*] Improve hight read throughput, static data. Use DAX caching layer / CACHING OR RESPONSES of API Gateway

### In this lecture
- Serverless REST API: HTTPS, API Gateway, Lambda, DynamoDB
- Using **Cognito to generate temporary credentials with STS** to access S3 bucket with restricted policy. App users can directly access AWS resources this way. Pattern can be applied to DynamoDB, Lambda…
- **Caching the reads on DynamoDB using DAX**
- **Caching the REST requests at the API Gateway level**
- Security for authentication and authorization with Cognito, STS

### Serverless hosted website: MyBlog.com
- This website should scale globally
- Blogs are rarely written, but often read
- Some of the website is purely static files, the rest is a dynamic REST API
- Caching must be implement where possible
- Any new users that subscribes should receive a welcome email
- Any photo uploaded to the blog should have a thumbnail generated


[*] Provide securit with CloudFront: OAI, origin access identity, + Bucket Policy

client <---> CloudFront <-----------------------> S3 (Policy only authorize from OAI)
                          Origin Access Identity

### AWS Hosted Website Summary
- We’ve seen static content being distributed using CloudFront with S3
- The REST API was serverless, didn’t need Cognito because public
- We leveraged a Global DynamoDB table to serve the data globally
- (we could have used Aurora Global Tables)
- We enabled DynamoDB streams to trigger a Lambda function
- The lambda function had an IAM role which could use SES
- SES (Simple Email Service) was used to send emails in a serverless way
- S3 can trigger SQS / SNS / Lambda to notify of events

### Micro Services architecture
- We want to switch to a micro service architecture
- Many services interact with each other directly using a REST API
- Each architecture for each micro service may vary in form and shape

- We want a micro-service architecture so we can have a leaner
development lifecycle for each service

### Discussions on Micro Services
- **You are free to design each micro-service the way you want**
- Synchronous patterns: API Gateway, Load Balancers
- Asynchronous patterns: SQS, Kinesis, SNS, Lambda triggers (S3)
- Challenges with micro-services:
  - repeated overhead for creating each new microservice,
  - issues with optimizing server density/utilization
  - complexity of running multiple versions of multiple microservices simultaneously
  - proliferation of client-side code requirements to integrate with many separate services.
- Some of the challenges are solved by Serverless patterns:
  - API Gateway, Lambda scale automatically and you pay per usage
  - You can easily clone API, reproduce environments
  - Generated client SDK through Swagger integration for the API Gateway

### Distributing paid content
- We sell videos online and users have to paid to buy videos
- Each videos can be bought by many different customers
- We only want to distribute videos to users who are premium users
- We have a database of premium users
- Links we send to premium users should be short lived
- Our application is global
- We want to be fully serverles

### Premium User Video service
- We have implemented a fully serverless solution:
  - Cognito for authentication
  - DynamoDB for storing users that are premium
  - 2 serverless applications
    - Premium User registration
    - CloudFront Signed URL generator
  - Content is stored in S3 (serverless and scalable)
  - Integrated with CloudFront with OAI for security (users can’t bypass)
  - CloudFront can only be used using Signed URLs to prevent unauthorized users
  - What about S3 Signed URL? They’re not efficient for global access

### Software updates offloading
- We have an application running on EC2, that distributes software updates once in a while
- When a new software update is out, we get a lot of request and the content is distributed in mass over the network. It’s very costly
- We don’t want to change our application, but want to optimize our cost and CPU, how can we do it?

### Why CloudFront?
- No changes to architecture
- Will cache software update files at the edge
- Software update files are not dynamic, they’re static (never changing)
- Our EC2 instances aren’t serverless
- But CloudFront is, and will scale for us
- Our ASG will not scale as much, and we’ll save tremendously in EC2
- We’ll also save in availability, network bandwidth cost, etc
- Easy way to make an existing application more scalable and cheaper!

### Big Data Ingestion Pipeline
- We want the ingestion pipeline to be fully serverless
- We want to collect data in real time
- We want to transform the data
- We want to query the transformed data using SQL
- The reports created using the queries should be in S3
- We want to load that data into a warehouse and create dashboards

------
Serverless Architectures Quiz

Question 1:
As a solutions architect, you have been tasked to implement a fully Serverless REST API. Which technology choices do you recommend?
A: API Gateway + AWS Lambda

Question 2:
Which technology does not have an out of the box caching feature?
A: Lambda

  Lambda does not have an out of the box caching feature (it's often paired with API gateway for that)

Question 3:
Which service allows to federate mobile users and generate temporary credentials so that they can access their own S3 bucket sub-folder?
A: Cognito

  in combination with STS

Question 4:
You would like to distribute your static content which currently lives in Amazon S3 to multiple regions around the world, such as the US, France and Australia. What do you recommend?
A: CloudFront

  This is a perfect use case for CloudFront

Question 5:
You have hosted a DynamoDB table in ap-northeast-1 and would like to make it available in eu-west-1. What must be enabled first to create a DynamoDB Global Table?
A: DynamoDB Streams.

  Streams enable DynamoDB to get a changelog and use that changelog to replicate data across regions

Question 6:
A Lambda function is triggered by a DynamoDB stream and is meant to insert data into SQS for further long processing jobs. The Lambda function does seem able to read from the DynamoDB stream but isn't able to store messages in SQS. What's the problem?
A: The Lambda IAM role is missing permissions

Question 7:
You would like to create a micro service whose sole purpose is to encode video files with your specific algorithm from S3 back into S3. You would like to make that micro-service reliable and retry upon failure. Processing a video may take over 25 minutes. The service is asynchronous and it should be possible for the service to be stopped for a day and resume the next day from the videos that haven't been encoded yet. Which of the following service would you recommend to implement this service?
A: X SQS + EC2

  SQS allows you to retain messages for days and process them later, while we take down our EC2 instances

Question 8:
You would like to distribute paid software installation files globally for your customers that have indeed purchased the content. The software may be purchased by different users, and you want to protect the download URL with security including IP restriction. Which solution do you recommend?
A: CloudFront Signed URL

  This will have security including IP restriction

Question 9:
You are a photo hosting service and publish every month a master pack of beautiful mountains images, that are over 50 GB in size and downloaded from all around the world. The content is currently hosted on EFS and distributed by ELB and EC2 instances. You are experiencing high load each month and very high network costs. What can you recommend that won't force an application refactor and reduce network costs and EC2 load dramatically?
A: Create a CloudFront distribution

  CloudFront can be used in front of an ELB

Question 10:
You would like to deliver big data streams in real time to multiple consuming applications, with replay features. Which technology do you recommend?
A: Kinesis Data Streams

------

## Databases

### Choosing the Right Database
- We have a lot of managed databases on AWS to choose from
- Questions to choose the right database based on your architecture:
  - Read-heavy, write-heavy, or balanced workload? Throughput needs? Will it
  change, does it need to scale or fluctuate during the day?
  - How much data to store and for how long? Will it grow? Average object size?
  How are they accessed?
  - Data durability? Source of truth for the data ?
  - Latency requirements? Concurrent users?
  - Data model? How will you query the data? Joins? Structured? Semi-Structured?
  - Strong schema? More flexibility? Reporting? Search? RDBMS / NoSQL?
  - License costs? Switch to Cloud Native DB such as Aurora?

### Database Types
- **RDBMS (= SQL / OLTP)**: RDS, Aurora – great for joins
- **NoSQL database**: DynamoDB (~JSON), ElastiCache (key / value pairs),
Neptune (graphs) – no joins, no SQL
- **Object Store**: S3 (for big objects) / Glacier (for backups / archives)
- **Data Warehouse** (= SQL Analytics / BI): Redshift (OLAP), Athena
- **Search**: ElasticSearch (JSON) – free text, unstructured searches
- **Graphs**: Neptune – displays relationships between data

### RDS Overview
- Managed PostgreSQL / MySQL / Oracle / SQL Server
- Must **provision an EC2 instance & EBS Volume type and size**
- Support for Read Replicas and Multi AZ
- Security through IAM, Security Groups, KMS, SSL in transit
- Backup / Snapshot / Point in time restore feature
- Managed and Scheduled maintenance
- Monitoring through CloudWatch

- **Use case**: Store relational datasets (RDBMS / OLTP), perform SQL queries,
transactional inserts / update / delete is available

### RDS for Solutions Architect
- **Operations**: small downtime when failover happens, when maintenance happens, scaling in read replicas / ec2 instance / restore EBS implies manual intervention, application changes
- **Security**: AWS responsible for OS security, we are responsible for setting
up KMS, security groups, IAM policies, authorizing users in DB, using SSL
- **Reliability**: Multi AZ feature, failover in case of failures
- **Performance**: depends on EC2 instance type, EBS volume type, ability to
add Read Replicas. Doesn’t auto-scale
- **Cost**: Pay per hour based on provisioned EC2 and EBS

### Aurora Overview
- Compatible API for PostgreSQL / MySQL
- Data is held in 6 replicas, across 3 AZ
- Auto healing capability
- Multi AZ, Auto Scaling Read Replicas
- Read Replicas can be Global
- Aurora database can be Global for DR or latency purposes
- Auto scaling of storage from 10GB to 64 TB
- Define EC2 instance type for aurora instances
- Same security / monitoring / maintenance features as RDS
- “Aurora Serverless” option

- **Use case**: same as RDS, but with less maintenance / more flexibility / more performance

### Aurora for Solutions Architect
- **Operations**: less operations, auto scaling storage
- **Security**: AWS responsible for OS security, we are responsible for setting
up KMS, security groups, IAM policies, authorizing users in DB, using SSL
- **Reliability**: Multi AZ, highly available, possibly more than RDS, Aurora
Serverless option.
- **Performance**: 5x performance (according to AWS) due to architectural
optimizations. Up to 15 Read Replicas (only 5 for RDS)
- **Cost**: Pay per hour based on EC2 and storage usage. Possibly lower
costs compared to Enterprise grade databases such as Oracle

### ElastiCache Overview
- Managed Redis / Memcached (similar offering as RDS, but for caches)
- In-memory data store, sub-millisecond latency
- Must provision an EC2 instance type
- Support for Clustering (Redis) and Multi AZ, Read Replicas (sharding)
- Security through IAM, Security Groups, KMS, Redis Auth
- Backup / Snapshot / Point in time restore feature
- Managed and Scheduled maintenance
- Monitoring through CloudWatch

- **Use Case**: Key/Value store, Frequent reads, less writes, cache results for DB queries, store session data for websites, cannot use SQL.

## ElastiCache for Solutions Architect
- **Operations**: same as RDS
- **Security**: AWS responsible for OS security, we are responsible for setting
up KMS, security groups, IAM policies, users (Redis Auth), using SSL
- **Reliability**: Clustering, Multi AZ
- **Performance**: Sub-millisecond performance, in memory, read replicas for
sharding, very popular cache option
- **Cost**: Pay per hour based on EC2 and storage usage

### DynamoDB Overview
- AWS proprietary technology, managed NoSQL database
- Serverless, provisioned capacity, auto scaling, on demand capacity (Nov 2018)
- Can replace ElastiCache as a key/value store (storing session data for example)
- Highly Available, Multi AZ by default, Read and Writes are decoupled, DAX for read cache
- Reads can be eventually consistent or strongly consistent
- Security, authentication and authorization is done through IAM
- DynamoDB Streams to integrate with AWS Lambda
- Backup / Restore feature, Global Table feature
- Monitoring through CloudWatch
- Can only query on primary key, sort key, or indexes

- **Use Case**: Serverless applications development (small documents 100s KB), distributed serverless cache, doesn’t have SQL query language available, has transactions capability from Nov 2018

### DynamoDB for Solutions Architect
- **Operations**: no operations needed, auto scaling capability, serverless
- **Security**: full security through IAM policies, KMS encryption, SSL in flight
- **Reliability**: Multi AZ, Backups
- **Performance**: single digit millisecond performance, DAX for caching
reads, performance doesn’t degrade if your application scales
- **Cost**: Pay per provisioned capacity and storage usage (no need to guess
in advance any capacity – can use auto scaling)

## S3 Overview
- S3 is a… key / value store for objects
- Great for big objects, not so great for small objects
- Serverless, scales infinitely, max object size is 5 TB
- Eventually consistency for overwrites and deletes
- Tiers: S3 Standard, S3 IA, S3 One Zone IA, Glacier for backups
- Features: Versioning, Encryption, Cross Region Replication, etc…
- Security: IAM, Bucket Policies, ACL
- Encryption: SSE-S3, SSE-KMS, SSE-C, client side encryption, SSL in transit

- **Use Case**: static files, key value store for big files, website hosting

## S3 for Solutions Architect
- **Operations**: no operations needed
- **Security**: IAM, Bucket Policies, ACL, Encryption (Server/Client), SSL
- **Reliability**: 99.999999999% durability / 99.99% availability, Multi AZ, CRR
- **Performance**: scales to thousands of read / writes per second, transfer
acceleration / multi-part for big files
- **Cost**: pay per storage usage, network cost, requests number

### Athena Overview
- Fully Serverless database with SQL capabilities
- Used to query data in S3
- Pay per query
- Output results back to S3
- Secured through IAM

- **Use Case**: one time SQL queries, serverless queries on S3, log analytics

### Athena for Solutions Architect
- **Operations**: no operations needed, serverless
- **Security**: IAM + S3 security
- **Reliability**: managed service, uses Presto engine, highly available
- **Performance**: queries scale based on data size
- **Cost**: pay per query / per TB of data scanned, serverless

### Redshift Overview
- Redshift is based on PostgreSQL, but **it’s not used for OLTP**
- **It’s OLAP – online analytical processing (analytics and data warehousing)**
- 10x better performance than other data warehouses, scale to PBs of data
- **Columnar** storage of data (instead of row based)
- Massively Parallel Query Execution (MPP), highly available
- Pay as you go based on the instances provisioned
- Has a SQL interface for performing the queries
- BI tools such as AWS Quicksight or Tableau integrate with it

### Redshift Continued…
- Data is loaded from S3, DynamoDB, DMS, other DBs…
- From 1 node to 128 nodes, up to 160 GB of space per node
- __Leader node__: for query planning, results aggregation
- __Compute node__: for performing the queries, send results to leader
- __Redshift Spectrum__: perform queries directly against S3 (no need to load)
- Backup & Restore, Security VPC / IAM / KMS, Monitoring
- Redshift Enhanced VPC Routing: COPY / UNLOAD goes through VPC

### Redshift – Snapshots & DR
- Snapshots are point-in-time backups of a cluster, stored internally in S3
- Snapshots are incremental (only what has changed is saved)
- You can restore a snapshot into a **new cluster**
- Automated: every 8 hours, every 5 GB, or on a schedule. Set retention
- Manual: snapshot is retained until you delete it

- **You can configure Amazon Redshift to automatically copy snapshots (automated or manual) of a cluster to another AWS Region**

Redshift Spectrum
- Query data that is already in S3 without loading it
- **Must have a Redshift cluster available to start the query**
- The query is then submitted to thousands of Redshift Spectrum nodes

https://aws.amazon.com/blogs/big-data/amazon-redshift-spectrum-extends-data-warehousing-out-to-exabytes-no-loading-required

### Redshift for Solutions Architect
- **Operations**: similar to RDS
- **Security**: IAM, VPC, KMS, SSL (similar to RDS)
- **Reliability**: highly available, auto healing features
- **Performance**: 10x performance vs other data warehousing, compression
- **Cost**: pay per node provisioned, 1/10th of the cost vs other warehouses

- **Remember: Redshift = Analytics / BI / Data Warehouse**

### Neptune
- Fully managed **graph** database
- **When do we use Graphs?**
  - High relationship data
  - Social Networking: Users friends with Users, replied to comment on post of user and likes other comments.
  - Knowledge graphs (Wikipedia)
- Highly available across 3 AZ, with up to 15 read replicas
- Point-in-time recovery, continuous backup to Amazon S3
- Support for KMS encryption at rest + HTTPS

### Neptune for Solutions Architect
- **Operations**: similar to RDS
- **Security**: IAM, VPC, KMS, SSL (similar to RDS) + IAM Authentication
- **Reliability**: Multi-AZ, clustering
- **Performance**: best suited for graphs, clustering to improve performance
- **Cost**: pay per node provisioned (similar to RDS)

- **Remember: Neptune = Graphs**

### ElasticSearch
- Example: In DynamoDB, you can only find by primary key or indexes.
- With ElasticSearch, you can search any field, even partially matches
- It’s common to use ElasticSearch as a complement to another database
- ElasticSearch also has some usage for Big Data applications
- You can provision a cluster of instances
- Built-in integrations: Amazon Kinesis Data Firehose, AWS IoT, and
Amazon CloudWatch Logs for data ingestion
- Security through Cognito & IAM, KMS encryption, SSL & VPC
- Comes with Kibana (visualization) & Logstash (log ingestion) – ELK stack

### ElasticSearch for Solutions Architect
- **Operations**: similar to RDS
- **Security**: Cognito, IAM, VPC, KMS, SSL
- **Reliability**: Multi-AZ, clustering
- **Performance**: based on ElasticSearch project (open source), petabyte scale
- **Cost**: pay per node provisioned (similar to RDS)

- **Remember: ElasticSearch = Search / Indexing**

-----
Databases Quiz

Question 1:
Which database helps you store data in a relational format, with SQL language compatibility and capability of processing transactions?
A: RDS

Question 2:
Which database do you suggest to have caching capability with a Redis compatible API?
A: ElascticCache

  ElastiCache can create a Redis cache or a Memcached cache

Question 3:
You are looking to perform OLTP, and would like to have the underlying storage with the maximum amount of replication and auto-scaling capability. What do you recommend?
A: Aurora

Question 4:
As a solution architect, you plan on creating a social media website where users can be friends with each other, and like each other's posts. You plan on performing some complicated queries such as "What are the number of likes on the posts that have been posted by the friends of Mike?". What database do you suggest?
A: Neptune

  This is AWS' managed graph database

Question 5:
You would like to store big objects of 100 MB into a reliable and durable Key Value store. What do you recommend?
A: S3

  S3 is indeed a key value store! (where the key is the full path of the object in the bucket)

Question 6:
You would like to have a database which is efficient at performing analytical queries on large sets of columnar data. You would like to connect that Data Warehouse to a reporting and dashboard tool such as Amazon Quicksight. Which technology do you recommend?
A: Redshift

Question 7:
Your log data is currently stored in S3 and you would like to perform a quick analysis if possible serverless to filter the logs and find a user which may have completed an unauthorized action. Which technology do you recommend?
A: Athena

Question 8:
Your gaming website is currently running on top of DynamoDB. Users have been asking for a search feature to find other gamers by name, with partial matches if possible. Which technology do you recommend to implement that feature?
A: ElasticSearch

  Anytime you see "search", think ElasticSearch

-----

## AWS Monitoring, Audit and Performance

### AWS CloudWatch Metrics
- CloudWatch provides metrics for every services in AWS
- **Metric** is a variable to monitor (CPUUtilization, NetworkIn…)
- Metrics belong to **namespaces**
- **Dimension** is an attribute of a metric (instance id, environment, etc…).
- Up to 10 dimensions per metric
- Metrics have **timestamps**
- Can create CloudWatch dashboards of metrics

### AWS CloudWatch EC2 Detailed monitoring
- EC2 instance metrics have metrics “every 5 minutes”
- With detailed monitoring (for a cost), you get data “every 1 minute”
- Use detailed monitoring if you want to more prompt scale your ASG!

- The AWS Free Tier allows us to have 10 detailed monitoring metrics

- **Note: EC2 Memory usage is by default not pushed (must be pushed from inside the instance as a custom metric)**

### AWS CloudWatch Custom Metrics
- Possibility to define and send your own custom metrics to CloudWatch
- Ability to use dimensions (attributes) to segment metrics
  - Instance.id
  - Environment.name
- Metric resolution (**StorageResolution** API parameter – two possible value):
  - Standard: 1 minute (60 seconds)
  - High Resolution: 1 second – Higher cost
- Use API call **PutMetricData**
- Use exponential back off in case of throttle errors

### CloudWatch Dashboards
- Great way to setup dashboards for quick access to keys metrics
- **Dashboards are global**
- **Dashboards can include graphs from different regions**
- You can change the time zone & time range of the dashboards
- You can setup automatic refresh (10s, 1m, 2m, 5m, 15m)

- Pricing:
- 3 dashboards (up to 50 metrics) for free
- $3/dashboard/month afterwards

### AWS CloudWatch Logs
- Applications can send logs to CloudWatch using the SDK
- CloudWatch can collect log from:
  - Elastic Beanstalk: collection of logs from application
  - ECS: collection from containers
  - AWS Lambda: collection from function logs
  - VPC Flow Logs: VPC specific logs
  - API Gateway
  - CloudTrail based on filter
  - CloudWatch log agents: for example on EC2 machines
  - Route53: Log DNS queries
- CloudWatch Logs can go to:
  - Batch exporter to S3 for archival
  - Stream to ElasticSearch cluster for further analytics

### AWS CloudWatch Logs
- Logs storage architecture:
  - Log groups: arbitrary name, usually representing an application
  - Log stream: instances within application / log files / containers
- Can define log expiration policies (never expire, 30 days, etc..)
- Using the AWS CLI we can tail CloudWatch logs
- To send logs to CloudWatch, make sure IAM permissions are correct!
- Security: encryption of logs using KMS at the Group Level

### CloudWatch Logs Metric Filter & Insights
- CloudWatch Logs can use filter expressions
  - For example, find a specific IP inside of a log
  - Metric filters can be used to trigger alarms

- CloudWatch Logs Insights (new – Nov 2018) can be used to query logs
and add queries to CloudWatch Dashboards

### AWS CloudWatch Alarms
- Alarms are used to trigger notifications for any metric
- Alarms can go to Auto Scaling, EC2 Actions, SNS notifications
- Various options (sampling, %, max, min, etc…)
- Alarm States:
  - OK
  - INSUFFICIENT_DATA (Missing data points)
  - ALARM
- Period:
  - Length of time in seconds to evaluate the metric
  - High resolution custom metrics: can only choose 10 sec or 30 sec

### AWS CloudWatch Events
- Source + Rule => Target

- Schedule: Cron jobs
- Event Pattern: Event rules to react to a service doing something
  - Ex: CodePipeline state changes!
- Triggers to Lambda functions, SQS/SNS/Kinesis Messages
- CloudWatch Event creates a small JSON document to give information
about the change

### AWS CloudTrail
- Provides governance, compliance and audit for your AWS Account
- CloudTrail is enabled by default!
- Get an history of events / API calls made within your AWS Account by:
  - Console
  - SDK
  - CLI
  - AWS Services
- Can put logs from CloudTrail into CloudWatch Logs
- **If a resource is deleted in AWS, look into CloudTrail first!**

### AWS Config
- Helps with auditing and recording compliance of your AWS resources
- Helps record configurations and changes over time
- Possibility of storing the configuration data into S3 (analyzed by Athena)
- Questions that can be solved by AWS Config:
  - Is there unrestricted SSH access to my security groups?
  - Do my buckets have any public access?
  - How has my ALB configuration changed over time?
- You can receive alerts (SNS notifications) for any changes
- AWS Config is a per-region service
- Can be aggregated across regions and accounts

AWS Config Resource - View compliance of a resource over time

### AWS Config Rules
- Can use AWS managed config rules (over 75)
- Can make custom config rules (must be defined in AWS Lambda)
  - Evaluate if each EBS disk is of type gp2
  - Evaluate if each EC2 instance is t2.micro
- Rules can be evaluated / triggered:
  - For each config change
  - And / or: at regular time intervals
  - Can trigger CloudWatch Events if the rule is non-compliant (and chain with Lambda)
- Rules can have auto remediations:
  - If a resource is not compliant, you can trigger an auto remediation
  - Ex: stop instances with non-approved tags
- **AWS Config Rules does not prevent actions from happening (no deny)**
- **Pricing**: no free tier, $2 per active rule per region per month

### CloudWatch vs CloudTrail vs Config
- CloudWatch
  - Performance monitoring (metrics, CPU, network, etc…) & dashboards
  - Events & Alerting
  - Log Aggregation & Analysis
- CloudTrail
  - Record API calls made within your Account by everyone
  - Can define trails for specific resources
  - Global Service
- Config
  - Record configuration changes
  - Evaluate resources against compliance rules
  - Get timeline of changes and compliance

### For an Elasctic Load Balancer
- CloudWatch:
  - Monitoring Incoming connections metic
  - Visualize error codes as a % over time
  - Make a dashboard to get an idea of your load blanacer performance
- Config:
  - Track security group rules for the load Balancer
  - Track configuration changes for the Load Balancer
  - Ensure an SSL certificate is alqways assigned to the Load Blanacer (compliace)
- CloudTrail:
  - Track who made any changes to the Load Balancer with API calls.

-----
Monitoring Quiz

Question 1:
We'd like to have CloudWatch Metrics for EC2 at a 1 minute rate. What should we do?
A: Enable Detailed Monitoring

  This is a paid offering and gives you EC2 metrics at a 1 minute rate

Question 2:
High Resolution Custom Metrics can have a minimum resolution of
A: 1 second

Question 3:
Your CloudWatch alarm is triggered and controls an ASG. The alarm should trigger 1 instance being deleted from your ASG, but your ASG has already 2 instances running and the minimum capacity is 2. What will happen?
A: The alarm will remain in "ALARM" state but never decrease the number of instances in my ASG

  The number of instances in an ASG cannot go below the minimum, even if the alarm would in theory trigger an instance termination

Question 4:
An Alarm on a High Resolution Metric can be triggered as often as
A:

Question 5:
You have made a configuration change and would like to evaluate the impact of it on the performance of your application. Which service do you use?
A: CloudWatch

  CloudWatch is used to monitor the applications performance / metrics

Question 6:
Someone has terminated an EC2 instance in your account last week, which was hosting a critical database. You would like to understand who did it and when, how can you achieve that?
A: Look a CloudTrail

  CloudTrail helps audit the API calls made within your account, so the database deletion API call will appear here (regardless if made from the console, the CLI, or an SDK)

Question 7:
You would like to ensure that over time, none of your EC2 instances expose the port 84 as it is known to have vulnerabilities with the OS you are using. What can you do to monitor this?
A: Setup Config Rules

Question 8:
You would like to evaluate the compliance of your resource's configurations over time. Which technology do you choose?
A: Config

-----

### AWS STS – Security Token Service
- **Allows to grant limited and temporary access to AWS resources.**
- Token is valid for up to one hour (must be refreshed)
- **AssumeRole**
  - Within your own account: for enhanced security
  - Cross Account Access: assume role in target account to perform actions there
- **AssumeRoleWithSAML**
  - return credentials for users logged with SAML
- **AssumeRoleWithWebIdentity**
  - return creds for users logged with an IdP (Facebook Login, Google Login, OIDC compatible…)
  - AWS recommends against using this, and using Cognito instead
- **GetSessionToken**
  - for MFA, from a user or AWS account root user

### Using STS to Assume a Role
- Define an IAM Role within your account or cross-account
- Define which principals can access this IAM Role
- Use AWS STS (Security Token Service) to retrieve credentials and impersonate the IAM Role you have access to **(AssumeRole API**)
- Temporary credentials can be valid between __15 minutes to 1 hour__

https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_aws-accounts.html

Identity Federation in AWS
- Federation lets users outside of AWS to assume
temporary role for accessing AWS resources.
- These users assume identity provided access role.
- Federations can have many flavors:
- SAML 2.0
- Custom Identity Broker
- Web Identity Federation with Amazon Cognito
- Web Identity Federation without Amazon Cognito
- Single Sign On
- Non-SAML with AWS Microsoft AD

- Using federation, you don’t need to create IAM users
(user management is outside of AWS)


SAML 2.0 Federation
- To integrate Active Directory / ADFS with AWS (or any SAML 2.0)
- Provides access to AWS Console or CLI (through temporary creds)
- No need to create an IAM user for each of your employees


### AWS Directory Services
- **AWS Managed Microsoft AD**
  - Create your own AD in AWS, manage users locally, supports MFA
  - Establish “trust” connections with your on- premise AD
- **AD Connector**
  - Directory Gateway (proxy) to redirect to on- premise AD
  - Users are managed on the on-premise AD
- **Simple AD**
  - AD-compatible managed directory on AWS
  - Cannot be joined with on-premise AD

### AWS Organizations
- Global service
- Allows to manage multiple AWS accounts
- The main account is the master account – you can’t change it
- Other accounts are member accounts
- Member accounts can only be part of one organization
- Consolidated Billing across all accounts - single payment method
- Pricing benefits from aggregated usage (volume discount for EC2, S3…)
- API is available to automate AWS account creation

### Multi Account Strategies
- Create accounts per department, per cost center, per dev / test /
prod, based on regulatory restrictions (using SCP), for better
resource isolation (ex: VPC), to have separate per-account service
limits, isolated account for logging

- Multi Account vs One Account Multi VPC
- Use tagging standards for billing purposes
- Enable CloudTrail on all accounts, send logs to central S3 account
- Send CloudWatch Logs to central logging account
- Establish Cross Account Roles for Admin purposes

### IAM Conditions

**aws:SourceIP**: restrict the client IP from
which the API calls are being made

**Aws:RequestedRegion**: restrict the region
The API calls are made to

**Restrict based on tags Force**
**MFA**

### IAM for S3
- ListBucket permission applies to
  arn:aws:s3:::test
- => bucket level permission

- GetObject, PutObject,
  DeleteObject applies to
  arn:awn:s3:::test/*
- => object level permission

------
Identity and Access Management (IAM) - Advanced - Quiz

Question 1:
We need to gain access to a Role in another AWS account. How is it done?
A: We should use the STS service to gain temporary credentials

  STS will allow us to get cross account access through the creation of a role in our account authorized to access a role in another account. See more here: https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html

Question 2:
You have a mobile application and would like to give your users access to their own personal space in Amazon S3. How do you achieve that?
A: Use Cognito Identity Federation

  Cognito is made to federate mobile user accounts and provide them with their own IAM policy. As such, they should be able thanks to that policy to access their own personal space in Amazon S3.

  X: Use SAML Identity Federation

    SAML identity federation is used to integrate a service such as Active Directory with AWS. It does not work for mobile applciations

Question 3:
You have strong regulatory requirements to only allow fully internally audited AWS Services in production. You still want to allow your teams to experiment in development environments while services are being audited. How can you best set this up?
A: Create an AWS Organization and create two Prod and Dev OU. Apply a SCP on Prod

Question 4:
[SAA-C02] You have an on-premise active directory setup and would like to provide access for your on-premise users to the multiple accounts you have in AWS. The solution should scale to adding accounts in the future. What do you recommend?
A: Setup AWS Single Sign-On

Question 5:
Which AWS Directory Service allows you to proxy requests to your on-premise active directory?
A: AD Connector
------

[*]

## Section 20: AWS Security & Encryption: KMS, SSM Parameter Store, CloudHSM, Shield, WAF

## AWS Security & Encryption

## Why encryption?

### Encryption in flight (SSL)
- Data is encrypted before sending and decrypted after receiving
- SSL certificates help with encryption (HTTPS)
- Encryption in flight ensures no MITM (man in the middle attack) can happen

## Why encryption?

### Server side encryption at rest
- Data is encrypted after being received by the server
- Data is decrypted before being sent
- It is stored in an encrypted form thanks to a key (usually a data key)
- The encryption / decryption keys must be managed somewhere and
the server must have access to it

## Why encryption?

### Client side encryption
- Data is encrypted by the client and never decrypted by the server
- Data will be decrypted by a receiving client
- The server should not be able to decrypt the data
- Could leverage Envelope Encryption

### AWS KMS (Key Management Service)
- Anytime you hear “encryption” for an AWS service, it’s most likely KMS
- Easy way to control access to your data, AWS manages keys for us
- Fully integrated with IAM for authorization
- Seamlessly integrated into:
  - Amazon EBS: encrypt volumes
  - Amazon S3: Server side encryption of objects
  - Amazon Redshift: encryption of data
  - Amazon RDS: encryption of data
  - Amazon SSM: Parameter store
  - Etc…
- But you can also use the CLI / SDK

### KMS – Customer Master Key (CMK) Types
- **Symmetric (AES-256 keys)**
  - First offering of KMS, single encryption key that is used to Encrypt and Decrypt
  - AWS services that are integrated with KMS use Symmetric CMKs
  - Necessary for envelope encryption
  - You never get access to the Key unencrypted (must call KMS API to use)
- **Asymmetric (RSA & ECC key pairs)**
  - Public (Encrypt) and Private Key (Decrypt) pair
  - Used for Encrypt/Decrypt, or Sign/Verify operations
  - The public key is downloadable, but you access the Private Key unencrypted
  - Use case: encryption outside of AWS by users who can’t call the KMS API

### AWS KMS (Key Management Service)
- Able to fully manage the keys & policies:
  - Create
  - Rotation policies
  - Disable
  - Enable
- Able to audit key usage (using CloudTrail)
- Three types of Customer Master Keys (CMK):
- AWS Managed Service Default CMK: free
  - User Keys created in KMS: $1 / month
  - User Keys imported (must be 256-bit symmetric key): $1 / month
  - + pay for API call to KMS ($0.03 / 10000 calls)

### AWS KMS 101
- Anytime you need to share sensitive information… use KMS
- Database passwords
- Credentials to external service
- Private Key of SSL certificates
- The value in KMS is that the CMK used to encrypt data can never be
retrieved by the user, and the CMK can be rotated for extra security

### AWS KMS 101
- **Never ever store your secrets in plaintext, especially in your code!**
- Encrypted secrets can be stored in the code / environment variables
- **KMS can only help in encrypting up to 4KB of data per call**
- If data > 4 KB, use envelope encryption

- To give access to KMS to someone:
  - Make sure the Key Policy allows the user
  - Make sure the IAM Policy allows the API calls

### KMS Key Policies
- Control access to KMS keys, “similar” to S3 bucket policies
- Difference: you cannot control access without them
- **Default KMS Key Policy:**
  - Created if you don’t provide a specific KMS Key Policy
  - Complete access to the key to the root user = entire AWS account
  - Gives access to the IAM policies to the KMS key
- **Custom KMS Key Policy:**
  - Define users, roles that can access the KMS key
  - Define who can administer the key
  - Useful for cross-account access of your KMS key

### Copying Snapshots across accounts
1. Create a Snapshot, encrypted with your own CMK
2. Attach a KMS Key Policy to authorize cross-account access
3. Share the encrypted snapshot
4. (in target) Create a copy of the Snapshot, encrypt it with a KMS Key in your account
5. Create a volume from the snapshot KMS Key Policy

### SSM Parameter Store
- Secure storage for configuration and secrets
- Optional Seamless Encryption using KMS
- Serverless, scalable, durable, easy SDK
- Version tracking of configurations / secrets
- Configuration management using path & IAM
- Notifications with CloudWatch Events
- Integration with CloudFormation

### SSM Parameter Store Hierarchy

### AWS Secrets Manager
- Newer service, meant for storing secrets
- Capability to **force rotation** of secrets every X days
- Automate generation of secrets on rotation (uses Lambda)
- Integration with **Amazon RDS** (MySQL, PostgreSQL, Aurora)
- Secrets are encrypted using KMS

- Mostly meant for RDS integration

### CloudHSM
- KMS => AWS manages the software for encryption
- CloudHSM => AWS provisions encryption **hardware**
- Dedicated Hardware (HSM = Hardware Security Module)
- You manage your own encryption keys entirely (not AWS)
- HSM device is tamper resistant, FIPS 140-2 Level 3 compliance
- **CloudHSM clusters are spread across Multi AZ (HA) – must setup**
- Supports both symmetric and **asymmetric** encryption (SSL/TLS keys)
- No free tier available
- Must use the CloudHSM Client Software
- Redshift supports CloudHSM for database encryption and key management
- Good option to use with SSE-C encryption

### AWS Shield
- **AWS Shield Standard:**
  - Free service that is activated for every AWS customer
  - Provides protection from attacks such as SYN/UDP Floods, Reflection attacks
  and other layer 3/layer 4 attacks
- **AWS Shield Advanced**:
  - Optional DDoS mitigation service ($3,000 per month per organization)
  - Protect against more sophisticated attack on Amazon EC2, Elastic Load
  Balancing (ELB), Amazon CloudFront, AWS Global Accelerator, and Route 53
  - 24/7 access to AWS DDoS response team (DRP)
  - Protect against higher fees during usage spikes due to DDoS

### AWS WAF – Web Application Firewall
- Protects your web applications from common web exploits (Layer 7)
- **Layer 7 is HTTP** (vs Layer 4 is TCP)
- Deploy on **Application Load Balancer, API Gateway, CloudFront**

- Define Web ACL (Web Access Control List):
  - Rules can include: **IP addresses**, HTTP headers, HTTP body, or URI strings
  - Protects from common attack - **SQL injection** and **Cross-Site Scripting (XSS)**
  - Size constraints, **geo-match (block countries)**
  - **Rate-based rules** (to count occurrences of events) – for DDoS protection

### AWS Firewall Manager
- Manage rules in all accounts of an AWS Organization

- Common set of security rules
- WAF rules (Application Load Balancer, API Gateways, CloudFront)
- AWS Shield Advanced (ALB, CLB, Elastic IP, CloudFront)
- Security Groups for EC2 and ENI resources in VPC

### AWS Shared Responsibility Model
- AWS responsibility - Security of the Cloud
- Protecting infrastructure (hardware, software, facilities, and networking) that runs
all of the AWS services
- Managed services like S3, DynamoDB, RDS etc
- Customer responsibility - Security in the Cloud
- For EC2 instance, customer is responsible for management of the guest OS
(including security patches and updates), firewall & network configuration, IAM
etc

### Example, for RDS
- AWS responsibility:
  - Manage the underlying EC2 instance, disable SSH access
  - Automated DB patching
  - Automated OS patching
  - Audit the underlying instance and disks & guarantee it functions
- Your responsibility:
  - Check the ports / IP / security group inbound rules in DB’s SG
  - In-database user creation and permissions
  - Creating a database with or without public access
  - Ensure parameter groups or DB is configured to only allow SSL connections
  - Database encryption setting

### Example, for S3
- AWS responsibility:
  - Guarantee you get unlimited storage
  - Guarantee you get encryption
  - Ensure separation of the data between different customers
  - Ensure AWS employees can’t access your data
- Your responsibility:
  - Bucket configuration
  - Bucket policy / public setting
  - IAM user and roles
  - Enabling encryption

### Shared Responsibility Model diagram

https://aws.amazon.com/compliance/shared-responsibility-model/

------
Security & Encryption Quiz

Question 1:
To enable encryption in flight, we need to have
A: an HTTPS endpoint with a SSL certificate

  encryption in flight = HTTPS, and HTTPs cannot be enabled without an SSL certificate

Question 2:
Server side encryption means that the data is sent encrypted to the server first
A: False

  Server side encryptions means the server will encrypt the data for us. We don't need to encrypt it beforehand

Question 3:
In server side encryption, only the encryption happens on the server. Where does the decryption happen?
A: The server

  In server side encryption, the decryption also happens on the server (in AWS, we wouldn't be able to decrypt the data ourselves as we can't have access to the corresponding encryption key)

Question 4:
In client side encryption, the server must know our encryption scheme to accept the data
A: False

  With client side encryption, the server does not need to know any information about the encryption being used, as the server won't perform any encryption or decryption tasks

Question 5:
We need to create User Keys in KMS before using the encryption features for EBS, S3, etc...
A: False

  we can use the AWS Managed Service Keys in KMS, therefore we don't need to create our own keys

Question 6:
We'd like our Lambda function to have access to a database password. We should
A: Have it as an encrypted environment variable and decrypt it at runtime

  This is the most secure solution amongst the options

Question 7:
We would like to audit the values of an encryption value over time
A: We should use SSM Parameter Store

  SSM Parameter Store has versioning and audit of values built-in directly

Question 8:
Under the shared responsibility model, what are you responsible for in RDS?
A: Security Group Rules

  This are configured by us and we've done that extensively in the course

Question 9:
Your user-facing website is a high risk target for DDoS attack and you would like to get 24/7 support in case they happen, as well as AWS bill reimbursement for the incurred costs during the attacks. What service should you use?
A: AWS Shield Advanced

Question 10:
You need an encryption service that supports asymmetric encryption schemes, and you want to manage the security keys yourself. Which service could you use?
A: CloudHSM

------

## Networking - VPC

### Understanding CIDR - IPv4
#### (Classless Inter-Domain Routing)
- CIDR are used for **Security Groups rules**, or **AWS networking in general**

- **They help to define an IP address range**
  - We’ve seen WW.XX.YY.ZZ/32 == one IP
  - We’ve seen 0.0.0.0/0 == all IPs
  - But we can define for ex: 192.168.0.0/26: 192.168.0.0 – 192.168.0.63 (64 IP)

### Understanding CIDR
- A CIDR has two components:
  - The base IP (XX.XX.XX.XX)
  - The Subnet Mask (/26)

- The base IP represents an IP contained in the range
- The subnet masks defines how many bits can change in the IP

- The subnet mask can take two forms. Examples:
  - 255.255.255.0 <- less common
  - /24           <- more common

### Understanding CIDRs
#### Subnet Masks
- The subnet masks basically allows part of the underlying IP to get additional next values from the base IP
- /32 allows for 1 IP = 2^0
- /31 allows for 2 IP = 2^1
- /30 allows for 4 IP = 2^2
- /29 allows for 8 IP = 2^3
- /28 allows for 16 IP = 2^4
- /27 allows for 32 IP = 2^5
- /26 allows for 64 IP = 2^6
- /25 allows for 128 IP = 2^7
- /24 allows for 256 IP = 2^8
- /16 allows for 65,536 IP = 2^16
- /0 allows for all IPs = 2^32

### Understanding CIDRs
#### Little exercise
- 192.168.0.0/24 = … ?
- 192.168.0.0 – 192.168.0.255 (256 IP)
- 192.168.0.0/16 = … ?
- 192.168.0.0 – 192.168.255.255 (65,536 IP)
- 134.56.78.123/32 = … ?
- Just 134.56.78.123
- 0.0.0.0/0
- All IP!
- When in doubt, use this website: https://www.ipaddressguide.com/cidr


### Private vs Public IP (IPv4)
### Allowed ranges
- The Internet Assigned Numbers Authority (IANA) established certain
blocks of IPV4 addresses for the use of private (LAN) and public
(Internet) addresses.

- Private IP can only allow certain values
  - 10.0.0.0 – 10.255.255.255 (10.0.0.0/8) <= in big networks
  - 172.16.0.0 – 172.31.255.255 (172.16.0.0/12) <= default AWS one
  - 192.168.0.0 – 192.168.255.255 (192.168.0.0/16) <= example: home networks

- All the rest of the IP on the internet are public IP

### Default VPC Walkthrough
- All new accounts have a default VPC
- New instances are launched into default VPC if no subnet is specified
- Default VPC have internet connectivity and all instances have public IP
- We also get a public and a private DNS name

### VPC in AWS – IPv4
- VPC = Virtual Private Cloud
- You can have multiple VPCs in a region (max 5 per region – soft limit)
  - Max CIDR per VPC is 5. For each CIDR:
  - Min size is /28 = 16 IP Addresses
- Max size is /16 = 65536 IP Addresses
  - Because VPC is private, only the Private IP ranges are allowed:
  - 10.0.0.0 – 10.255.255.255 (10.0.0.0/8)
  - 172.16.0.0 – 172.31.255.255 (172.16.0.0/12)
  - 192.168.0.0 – 192.168.255.255 (192.168.0.0/16)
- __Your VPC CIDR should not overlap with your other networks (ex: corporate)__

### Subnets - IPv4
- AWS reserves 5 IPs address (first 4 and last 1 IP address) in each Subnet
- These 5 IPs are not available for use and cannot be assigned to an instance
- Ex, if CIDR block 10.0.0.0/24, reserved IP are:
  - 10.0.0.0: Network address
  - 10.0.0.1: Reserved by AWS for the VPC router
  - 10.0.0.2: Reserved by AWS for mapping to Amazon-provided DNS
  - 10.0.0.3: Reserved by AWS for future use
  - 10.0.0.255: Network broadcast address. AWS does not support broadcast in a VPC,
  therefore the address is reserved

- Exam Tip: [*]
  - If you need 29 IP addresses for EC2 instances, you can’t choose a Subnet of size /27 (32 IP)
  - You need at least 64 IP, Subnet size /26 (64-5 = 59 > 29, but 32-5 = 27 < 29)

### Internet Gateways
- Internet gateways helps our VPC instances connect with the internet
- It scales horizontally and is HA (High Ability) and redundant
- Must be created separately from VPC
- One VPC can only be attached to one IGW and vice versa [*]
- Internet Gateway is also a NAT for the instances that have a public IPv4

- Internet Gateways on their own do not allow internet access…
- Route tables must also be edited!

### NAT Instances – Network Address Translation
(outdated but still at the exam)
- Allows instances in the private subnets to connect to the internet
- Must be launched in a public subnet
- Must disable EC2 flag: Source / Destination Check
- Must have Elastic IP attached to it
- Route table must be configured to route traffic from private subnets to

### NAT Instances – Comments
- Amazon Linux AMI pre-configured are available
- Not highly available / resilient setup out of the box
- => Would need to create ASG in multi AZ + resilient user-data script
- Internet traffic bandwidth depends on EC2 instance performance
- Must manage security groups & rules:
  - Inbound:
    - Allow HTTP / HTTPS Traffic coming from Private Subnets
    - Allow SSH from your home network (access is provided through Internet Gateway)
  - Outbound:
    - Allow HTTP / HTTPS traffic to the internet

### NAT Gateway
- AWS managed NAT, higher bandwidth, better availability, no admin
- Pay by the hour for usage and bandwidth
- NAT is created in a specific AZ, uses an EIP
- Cannot be used by an instance in that subnet (only from other subnets)
- Requires an IGW (Private Subnet => NAT => IGW)
- 5 Gbps of bandwidth with automatic scaling up to 45 Gbps
- No security group to manage / required

### NAT Instance vs Gateway
- See: https://docs.aws.amazon.com/vpc/latest/userguide/vpc-natcomparison.html

### DNS Resolution in VPC
- **enableDnsSupport: (= DNS Resolution setting)**
  - Default True
  - Helps decide if DNS resolution is supported for the VPC
  - If True, queries the AWS DNS server at 169.254.169.253
- **enableDnsHostname: (= DNS Hostname setting)**
  - False by default for newly created VPC, True by default for Default VPC
  - Won’t do anything unless enableDnsSupport=true
  - If True, Assign public hostname to EC2 instance if it has a public
- **If you use custom DNS domain names in a private zone in Route 53, you must set both these attributes to true**

[*]
Network ACLs & Security Group
Incoming Request

### Network ACLs
- NACL are like a firewall which control traffic from and to subnet
- Default NACL allows everything outbound and everything inbound
- **One NACL per Subnet, new Subnets are assigned the Default NACL**
- Define NACL rules:
  - Rules have a number (1-32766) and higher precedence with a lower number
  - E.g. If you define #100 ALLOW <IP> and #200 DENY <IP> , IP will be allowed
  - Last rule is an asterisk (*) and denies a request in case of no rule match
  - AWS recommends adding rules by increment of 100
- Newly created NACL will deny everything
- NACL are a great way of blocking a specific IP at the subnet level

#### Network ACLs vs Security Groups
https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html#VPC_Security_Comparison

#### Example Network ACL with Ephemeral Ports
- https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html

### VPC Peering [*]
- Connect two VPC, privately using AWS’ network
- Make them behave as if they were in the same network
- Must not have overlapping CIDR
- VPC Peering connection is not **transitive** (must be established for each VPC that need to communicate with one another) [*]
- You can do VPC peering with another AWS account
- **You must update route tables in __each VPC’s subnets__ to ensure instances can communicate** [*]

### VPC Peering – Good to know
- VPC peering can work **inter-region, cross-account**
- You can reference a security group of a peered VPC (works cross account)

### VPC Endpoints
- Endpoints allow you to connect to AWS Services using a private network
instead of the public www network
- They scale horizontally and are redundant
- They remove the need of IGW, NAT, etc… to access AWS Services
- **__Interface__**: provisions an ENI (private IP address) as an entry point (must
attach security group) – most AWS services
- **__Gateway__**: provisions a target and must be used in a route table – S3 and
DynamoDB
- In case of issues:
  - Check DNS Setting Resolution in your VPC
  - Check Route Tables

### Flow Logs
- Capture information about IP traffic going into your interfaces:
  - __VPC Flow Logs__
  - __Subnet Flow Logs__
  - __Elastic Network Interface Flow Logs__
- Helps to monitor & troubleshoot connectivity issues
- Flow logs data can go to S3 / CloudWatch Logs
- Captures network information from AWS managed interfaces too: ELB,
  RDS, ElastiCache, Redshift, WorkSpaces

[*] To use private DNS names, ensure that the attributes 'Enable DNS hostnames' and 'Enable DNS Support' are set to 'true' for your VPC (vpc-f4858893). Learn more.

### Flow Log Syntax
- <version> <account-id> <interface-id> <srcaddr> <dstaddr> <srcport>
<dstport> <protocol> <packets> <bytes> <start> <end> <action> <log- status>
- Srcaddr, dstaddr help identify problematic IP
- Srcport, dstport help identity problematic ports
- Action : success or failure of the request due to Security Group / NACL
- Can be used for analytics on usage patterns, or malicious behavior
- Flow logs example: https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html#flow-log-records

- **Query VPC flow logs using Athena on S3 or CloudWatch Logs Insights**

### Bastion Hosts
- We can use a Bastion Host to SSH into our private instances
- The bastion is in the public subnet which is then connected to all other private
subnets
- **Bastion Host security group must be tightened**

- Exam Tip: Make sure the bastion host only has port 22 traffic from the IP you need, not from the security groups of your other instances [*]

### Site to Site VPN
- Virtual Private Gateway:
  - VPN concentrator on the AWS side of the VPN connection
  - VGW is created and attached to the VPC from which you want to create the Site-toSite VPN connection
  - Possibility to customize the ASN
- Customer Gateway:
  - Software application or physical device on customer side of the VPN connection
  - https://docs.aws.amazon.com/vpc/latest/adminguide/Introduction.html#DevicesTested
  - IP Address: [*]
    - Use static, internet-routable IP address for your customer gateway device.
    - If behind a CGW behind NAT (with NAT-T), use the public IP address of the NAT

### Direct Connect
- Provides a dedicated **__private__** connection from a remote network to your VPC
- Dedicated connection must be setup between your DC and AWS Direct
Connect locations
- You need to setup a Virtual Private Gateway on your VPC
- Access public resources (S3) and private (EC2) on same connection
- Use Cases:
  - Increase bandwidth throughput - working with large data sets – lower cost
  - More consistent network experience - applications using real-time data feeds
  - Hybrid Environments (on prem + cloud)
- Supports both IPv4 and IPv6


Direct Connect Gateway
- If you want to setup a Direct Connect to one or more VPC in many
different regions (same account), you must use a Direct Connect Gateway

Direct Connect – Connection Types
- Dedicated Connections: 1Gbps and 10 Gbps capacity
- Physical ethernet port dedicated to a customer
- Request made to AWS first, then completed by AWS Direct Connect Partners
- Hosted Connections: 50Mbps, 500 Mbps, to 10 Gbps
- Connection requests are made via AWS Direct Connect Partners
- Capacity can be added or removed on demand
- 1, 2, 5, 10 Gbps available at select AWS Direct Connect Partners
- Lead times are often longer than 1 month to establish a new connection

### Direct Connect
– Encryption
- Data in transit is not encrypted but is
private
- AWS Direct Connect + VPN
provides an IPsec
-encrypted private
connection
- Good for an extra level of security,
but slightly more complex to put in
place

### Egress Only Internet Gateway
- Egress only Internet Gateway is for IPv6 only
- Similar function as a NAT, but a NAT is for IPv4
- Good to know: IPv6 are all public addresses
- Therefore all our instances with IPv6 are publicly accessibly
- Egress Only Internet Gateway gives our IPv6 instances access to the
internet, but they won’t be directly reachable by the internet
- After creating an Egress Only Internet Gateway, edit the route tables

[SAA-C02]
## AWS PrivateLink (VPC Endpoint Services) [*]
- Most secure & scalable way to expose a service to 1000s of VPC (own or other accounts)
- Does not require VPC peering, internet gateway, NAT, route tables…
- Requires a network load balancer (Service VPC) and ENI (Customer VPC)
- If the NLB is in multiple AZ, and the ENI in multiple AZ, the solution is fault tolerant!

[SAA-C02]
### EC2-Classic & AWS ClassicLink (deprecated)
- EC2-Classic: instances run in a single network shared with other customers
- Amazon VPC: your instances run logically isolated to your AWS account

- ClassicLink allows you to link EC2-Classic instances to a VPC in your account
  - Must associate a security group
  - Enables communication using private IPv4 addresses
  - Removes the need to make use of public IPv4 addresses or Elastic IP addresses

- Likely to be distractors at the exam

[SAA-C02]
## AWS VPN CloudHub
- Provide secure communication between sites, if you have multiple VPN connections

- Low cost hub-and-spoke model for primary or secondary network connectivity between locations

- It’s a VPN connection so it goes over the public internet

[SAA-C02]
### Transit Gateway
- **For having transitive peering between thousands of VPC and on-premises, hub-and-spoke (star) connection**
- Regional resource, can work cross -region
- Share cross -account using Resource Access Manager (RAM)
- You can peer Transit Gateways across regions
- Route Tables: limit which VPC can talk with other VPC
- Works with Direct Connect Gateway, VPN connections
- Supports **IP Multicast** (not supported by any other AWS service)

## VPC Section Summary (1/3)
- CIDR: IP Range
- VPC: Virtual Private Cloud => we define a list of IPv4 & IPv6 CIDR
- Subnets:Tied to an AZ, we define a CIDR
- Internet Gateway: at the VPC level, provide IPv4 & IPv6 Internet Access
- Route Tables: must be edited to add routes from subnets to the IGW, VPC Peering Connections, VPC Endpoints, etc…
- NAT Instances: gives internet access to instances in private subnets. Old, must be setup in a public subnet, disable Source / Destination check flag
- NAT Gateway: managed by AWS, provides scalable internet access to private instances, IPv4 only
- Private DNS + Route 53: enable DNS Resolution + DNS hostnames (VPC)
- NACL: Stateless, subnet rules for inbound and outbound, don’t forget ephemeral ports
- Security Groups: Stateful, operate at the EC2 instance level

## VPC Section Summary (2/3)
- VPC Peering: Connect two VPC with non overlapping CIDR, non transitive
- VPC Endpoints: Provide private access to AWS Services (S3, DynamoDB, CloudFormation, SSM) within VPC
- VPC Flow Logs: Can be setup at the VPC / Subnet / ENI Level, for ACCEPT and REJECT traffic, helps identifying attacks, analyze using Athena or CloudWatch Log Insights
- Bastion Host: Public instance to SSH into, that has SSH connectivity to instances in private subnets
- Site to Site VPN: setup a Customer Gateway on DC, a Virtual Private Gateway on VPC, and site-to-site VPN over public internet
- Direct Connect: setup a Virtual Private Gateway on VPC, and establish a direct private connection to an AWS Direct Connect Location
- Direct Connect Gateway: setup a Direct Connect to many VPC in different regions
- Internet Gateway Egress: like a NAT Gateway, but for IPv6

## VPC Section Summary (3/3)
- Private Link / VPC Endpoint Services:
- connect services privately from your service VPC to customers VPC
- Doesn’t need VPC peering, public internet, NAT gateway, route tables
- Must be used with Network Load Balancer & ENI
- ClassicLink: connect EC2-Classic instances privately to your VPC
- VPN CloudHub: hub-and-spoke VPN model to connect your sites
- Transit Gateway: transitive peering connections for VPC, VPN & DX

------
VPC Quiz
Question 1:
What does this CIDR correspond to?
10.0.4.0/28
A: 10.0.4.0 TO 10.0.4.15

  /28 means 16 IPs (=2^(32-28) = 2^4), means only the last digit can change.

Question 2:
You have a corporate network of size 10.0.0.0/8  and a satellite office of size 192.168.0.0/16. Which CIDR is acceptable for your AWS VPC if you plan on connecting your networks later on?
a: 172.16.0.0/16
  X: Lecture 222
  CIDR not should overlap, and the max CIDR size in AWS is /16

Question 3:
You plan on creating a subnet and want it to have at least capacity for 28 EC2 instances. What's the minimum size you need to have for your subnet?
A: /26

  perfect size (64 IP)

Question 4:
You have set up an internet gateway in your VPC, but your EC2 instances still don't have access to the internet. What is NOT a possible issue?
A: The security group does not allow network in.
  X: 228
  security groups are stateful and if traffic can go out, then it can go back in

Question 5:
You would like to provide internet access to your instances in private subnets with IPv4, while making sure this solution requires the least amount of administration and scales seamlessly. What should you use?
A: NAT Gateway

Question 6:
VPC Peering has been enabled between VPC A and VPC B, and the route tables have been updated for VPC A. Still, your instances cannot communicate. What is the likely issue?
A: Check the route tables in VPC B

  Route tables must be updated in both VPC that are peered

Question 7:
You have set-up a direct connection between your Corporate Data Center and your VPC A. You need to access VPC B in another region from your Corporate Data Center as well. What should you do?
A: Use a Direct Connect Gateway

  This is the main use case of Direct Connect Gateways

Question 8:
Which are the only two services that have a Gateway Endpoint instead of an Interface Endpoint as a VPC endpoint?
A: Amazon S3 & DynamoDB

  these two services have a Gateway endpoint (remember it), all the other ones have an interface endpoint (powered by Private Link - means a private IP)

Question 9:
Your company has created a REST API that it will sell to hundreds of customers as a SaaS. Your customers are on AWS and are using their own VPC. You would like to allow your customers to access your SaaS without going through the public internet while ensuring your infrastructure is not left exposed to network attacks. What do you recommend?
A: AWS PrivateLink

Question 10:
Your company has several on-premise sites across the USA. These sites are currently linked using a private connection, but your private connection provider has been recently quite unstable, making your IT architecture partially offline. You would like to create a backup connection that will use the public internet to link your on-premise sites, that you can failover in case of issues with your provider. What do you recommend?
A: VPN CloudHub

------

### Networking Costs in AWS per GB - Simplified
- Use Private IP instead of Public IP for good savings and better network performance
- Use same AZ for maximum savings (at the cost of high availability)


## Disaster Recovery Overview
- Any event that has a negative impact on a company’s business continuity or finances is a disaster
- Disaster recovery (DR) is about preparing for and recovering from a disaster
- What kind of disaster recovery?
- On-premise => On-premise: traditional DR, and very expensive
- On-premise => AWS Cloud: hybrid recovery
- AWS Cloud Region A => AWS Cloud Region B
- Need to define two terms:
- RPO: Recovery Point Objective
- RTO: Recovery Time Objective

### Disaster Recovery Strategies
- Backup and Restore
- Pilot Light
- Warm Standby
- Hot Site / Multi Site Approach

### Disaster Recovery Tips
- **Backup**
  - EBS Snapshots, RDS automated backups / Snapshots, etc…
  - Regular pushes to S3 / S3 IA / Glacier, Lifecycle Policy, Cross Region Replication
  - From On-Premise: Snowball or Storage Gateway
- **High Availability**
  - Use Route53 to migrate DNS over from Region to Region
  - RDS Multi-AZ, ElastiCache Multi-AZ, EFS, S3
  - Site to Site VPN as a recovery from Direct Connect
- **Replication**
  - RDS Replication (Cross Region), AWS Aurora + Global Databases
  - Database replication from on-premise to RDS
  - Storage Gateway
- **Automation**
  - CloudFormation / Elastic Beanstalk to re-create a whole new environment
  - Recover / Reboot EC2 instances with CloudWatch if alarms fail
  - AWS Lambda functions for customized automations
- **Chaos**
  - Netflix has a “simian-army” randomly terminating EC2


### DMS – Database Migration Service
- Quickly and securely migrate databases to AWS, resilient, self healing
- The source database remains available during the migration
- Supports:
  - Homogeneous migrations: ex Oracle to Oracle
  - Heterogeneous migrations: ex Microsoft SQL Server to Aurora
- Continuous Data Replication using CDC
- You must create an EC2 instance to perform the replication tasks


### DMS Sources and Targets
SOURCES:
- On-Premise and EC2 instances databases: Oracle, MS SQL Server,
MySQL, MariaDB, PostgreSQL, MongoDB, SAP, DB2
- Azure: Azure SQL Database
- Amazon RDS: all including Aurora
- Amazon S3
TARGETS:
- On-Premise and EC2 instances databases: Oracle, MS SQL Server, MySQL, MariaDB, PostgreSQL, SAP
- Amazon RDS
- Amazon Redshift
- Amazon DynamoDB
- Amazon S3
- ElasticSearch Service
- Kinesis Data Streams
- DocumentDB

[SAA-C02]
### AWS Schema Conversion Tool (SCT)
- Convert your Database’s Schema from one engine to another
- Example OLTP: (SQL Server or Oracle) to MySQL, PostgreSQL, Aurora
- Example OLAP: (Teradata or Oracle) to Amazon Redshift
- You do not need to use SCT if you are migrating the same DB engine
  - Ex: On-Premise PostgreSQL => RDS PostgreSQL
  - The DB engine is still PostgreSQL (RDS is the platform)

[SAA-C02]
### On-Premise strategy with AWS
- Ability to download Amazon Linux 2 AMI as a VM (.iso format)
  - VMWare, KVM, VirtualBox (Oracle VM), Microsoft Hyper-V
- VM Import / Export
  - Migrate existing applications into EC2
  - Create a DR repository strategy for your on-premise VMs
  - Can export back the VMs from EC2 to on-premise
- AWS Application Discovery Service
  - Gather information about your on-premise servers to plan a migration
  - Server utilization and dependency mappings
  - Track with AWS Migration Hub
- AWS Database Migration Service (DMS)
  - replicate On-premise => AWS , AWS => AWS, AWS => On-premise
  - Works with various database technologies (Oracle, MySQL, DynamoDB, etc..)
- AWS Server Migration Service (SMS)
  - Incremental replication of on-premise live servers to AWS

[SAA-C02]
### AWS DataSync
- Move large amount of data from on- premise to AWS
- Can synchronize to: **Amazon S3, Amazon EFS, Amazon FSx for Windows**
- Move data from your NAS or file system via **NFS** or **SMB**
- Replication tasks can be scheduled
hourly, daily, weekly
- Leverage the DataSync agent to
connect to your systems
https://docs.aws.amazon.com/datasync/latest/userguide/how-datasync-works.html
NFS / SMB to AWS (S3, EFS, FSx for Windows)
EFS to EFS

[SAA-C02]
### Transferring large amount of data into AWS
- Example: transfer 200 TB of data in the cloud. We have a 100 Mbps internet
connection.
- Over the internet / Site-to-Site VPN:
  - Immediate to setup
  - Will take 200(TB)*1000(GB)*1000(MB)*8(Mb)/100 Mbps = 16,000,000s = 185d
- Over direct connect 1Gbps:
  - Long for the one-time setup (over a month)
  - Will take 200(TB)*1000(GB)*8(Gb)/1 Gbps = 1,600,000s = 18.5d
- Over Snowball:
  - Will take 2 to 3 snowballs in parallel
  - Takes about 1 week for the end-to-end transfer
  - Can be combined with DMS
- For on-going replication / transfers: Site-to-Site VPN or DX with DMS or DataSync

------

Disaster Recovery Quiz

Question 1:
As part of your disaster recovery strategy, you would like to have only the critical systems up and running in AWS. You don't mind a longer RTO. Which DR strategy do you recommend?
A: Pilot Light

  If you're interested into reading more about disaster recovery, the whitepaper is here: https://d1.awsstatic.com/asset-repository/products/CloudEndure/CloudEndure_Affordable_Enterprise-Grade_Disaster_Recovery_Using_AWS.pdf

Question 2:
You would like to get the DR strategy with the lowest RTO and RPO, regardless of the cost, which one do you recommend?
A: Multi Site

  If you're interested into reading more about disaster recovery, the whitepaper is here: https://d1.awsstatic.com/asset-repository/products/CloudEndure/CloudEndure_Affordable_Enterprise-Grade_Disaster_Recovery_Using_AWS.pdf

Question 3:
Which of the following strategies has a potentially high RPO and RTO?
A: Backup and Restore

  If you're interested into reading more about disaster recovery, the whitepaper is here: https://d1.awsstatic.com/asset-repository/products/CloudEndure/CloudEndure_Affordable_Enterprise-Grade_Disaster_Recovery_Using_AWS.pdf

------

## Section 23: More Solution Architectures

### Extra Solution Architecture discussions - 249

[SAA-C02]
### S3 Events
- S3:ObjectCreated, S3:ObjectRemoved,
  S3:ObjectRestore, S3:Replication…
- Object name filtering possible (*.jpg)
- Use case: generate thumbnails of images uploaded to S3
- Can create as many “S3 events” as desired
- S3 event notifications typically deliver events in seconds but can sometimes take a minute or longer
- If two writes are made to a single non- versioned object at the same time, it is
possible that only a single event notification will be sent
- If you want to ensure that an event notification is sent for every successful write, you can enable versioning on your bucket

[SAA-C02]
### High Performance Computing (HPC)
- The cloud is the perfect place to perform HPC
- You can create a very high number of resources in no time
- You can speed up time to results by adding more resources
- You can pay only for the systems you have used

- Perform genomics, computational chemistry, financial risk modeling, weather prediction, machine learning, deep learning, autonomous driving

- Which services help perform HPC?

### Data Management & Transfer
- **AWS Direct Connect**:
  - Move GB/s of data to the cloud, over a private secure network
- **Snowball & Snowmobile**
  - Move PB of data to the cloud
- **AWS DataSync**
  - Move large amount of data between on-premise and S3, EFS, FSx for Windows

[SAA-C02][*]
### Compute and Networking
- EC2 Enhanced Networking (SR-IOV)
  - Higher bandwidth, higher PPS (packet per second), lower latency
  - Option 1: Elastic Network Adapter (ENA) up to 100 Gbps
  - Option 2: Intel 82599 VF up to 10 Gbps – LEGACY

- **Elastic Fabric Adapter** (EFA)
  - Improved ENA for HPC, only works for Linux
  - Great for inter-node communications, tightly coupled workloads
  - Leverages Message Passing Interface (MPI) standard
  - Bypasses the underlying Linux OS to provide low-latency, reliable transport

[SAA-C02]
### Storage
- Instance-attached storage:
  - EBS: scale up to 64000 IOPS with io1 Provisioned IOPS
  - Instance Store: scale to millions of IOPS, linked to EC2 instance, low latency
- Network storage:
  - Amazon S3: large blob, not a file system
  - Amazon EFS: scale IOPS based on total size, or use provisioned IOPS
  - Amazon FSx for Lustre:
    - HPC optimized distributed file system, millions of IOPS
    - Backed by S3

[SAA-C02]
### Automation and Orchestration
- AWS Batch
  - **AWS Batch** supports multi-node parallel jobs, which enables you to run single
  jobs that span multiple **EC2** instances.
  - Easily schedule jobs and launch EC2 instances accordingly

- AWS ParallelCluster
  - Open source cluster management tool to deploy HPC on AWS
  - Configure with text files
  - Automate creation of VPC, Subnet, cluster type and instance types

------

More Solution Architectures - Quiz
Quiz 22

Question 1:
Your Lambda function is processing events coming through S3 events and distributed through an SNS topic. You have decided to ensure that events that can not be processed are sent to a DLQ. In which service should you set up the DLQ?
A: Lambda function

  the invocation is asynchronous (coming from the SNS topic) so the DLQ has to be set on the Lambda side

Question 2:
You have created an architecture including CloudFront with WAF, Shield, an ALB, and EC2 instances. You would like to block an IP, where should you do it?
A: WAF

Question 3:
Your instances are deployed in an EC2 placement group of type cluster in order to perform HPC. You would like to maximize network performance between your instances. What should you use?
A: Elastic Fabric Adapar

------

Section 24: Other Services

### Continuous Integration
- Developers push the code to a code repository often (GitHub / CodeCommit /
Bitbucket / etc…)
- A testing / build server checks the code as soon as it’s pushed (CodeBuild / Jenkins CI / etc…)
- The developer gets feedback about the tests and checks that have passed / failed
- Find bugs early, fix bugs
- Deliver faster as the code is tested
- Deploy often
- Happier developers, as they’re unblocked

### Continuous Delivery
- Ensure that the software can be released reliably whenever needed.
- Ensures deployments happen often and are quick
- Shift away from “one release every 3 months” to ”5 releases a day”
- That usually means automated deployment
  - CodeDeploy
  - Jenkins CD
  - Spinnaker
  - Etc…

### Infrastructure as Code
- Currently, we have been doing a lot of manual work
- All this manual work will be very tough to reproduce:
- In another region
- in another AWS account
- Within the same region if everything was deleted
- Wouldn’t it be great, if all our infrastructure was… code?
- That code would be deployed and create / update / delete our
infrastructure

### What is CloudFormation
- CloudFormation is a declarative way of outlining your AWS
Infrastructure, for any resources (most of them are supported).
- For example, within a CloudFormation template, you say:
  - I want a security group
  - I want two EC2 machines using this security group
  - I want two Elastic IPs for these EC2 machines
  - I want an S3 bucket
  - I want a load balancer (ELB) in front of these machines

- Then CloudFormation creates those for you, in the right order, with the
exact configuration that you specify

### Benefits of AWS CloudFormation (1/2)
- Infrastructure as code
- No resources are manually created, which is excellent for control
- The code can be version controlled for example using git
- Changes to the infrastructure are reviewed through code
- Cost
- Each resources within the stack is tagged with an identifier so you can easily see how
much a stack costs you
- You can estimate the costs of your resources using the CloudFormation template
- Savings strategy: In Dev, you could automation deletion of templates at 5 PM and
recreated at 8 AM, safely

### Benefits of AWS CloudFormation (2/2)
- Productivity
- Ability to destroy and re-create an infrastructure on the cloud on the fly
- Automated generation of Diagram for your templates!
- Declarative programming (no need to figure out ordering and orchestration)
- Separation of concern: create many stacks for many apps, and many layers. Ex:
- VPC stacks
- Network stacks
- App stacks
- Don’t re-invent the wheel
- Leverage existing templates on the web!
- Leverage the documentation

### How CloudFormation Works
- Templates have to be uploaded in S3 and then referenced in
CloudFormation
- To update a template, we can’t edit previous ones. We have to reupload a new version of the template to AWS
- Stacks are identified by a name
- Deleting a stack deletes every single artifact that was created by
CloudFormation.

### Deploying CloudFormation templates
- Manual way:
- Editing templates in the CloudFormation Designer
- Using the console to input parameters, etc
- Automated way:
- Editing templates in a YAML file
- Using the AWS CLI (Command Line Interface) to deploy the templates
- Recommended way when you fully want to automate your flow

### CloudFormation Building Blocks
Templates components
1. Resources: your AWS resources declared in the template (MANDATORY)
2. Parameters: the dynamic inputs for your template
3. Mappings: the static variables for your template
4. Outputs: References to what has been created
5. Conditionals: List of conditions to perform resource creation
6. Metadata
Templates helpers:
1. References
2. Functions

### Note:
This is an introduction to CloudFormation
- It can take over 3 hours to properly learn and master CloudFormation
- This lecture is meant so you get a good idea of how it works
- The exam expects you to understand how to read CloudFormation

[SAA-C02]
### CloudFormation - StackSets
- Create, update, or delete stacks across **multiple accounts and regions** with a single operation
- Administrator account to create StackSets
- Trusted accounts to create, update,
delete stack instances from StackSets
- When you update a stack set, all associated stack instances are updated throughout all accounts and regions.

[*]
### AWS ECS – Elastic Container Service
- ECS is a container orchestration service
- ECS helps you run Docker containers on EC2 machines
- ECS is complicated, and made of:
  - “ECS Core”: Running ECS on user-provisioned EC2 instances
  - Fargate: Running ECS tasks on AWS-provisioned compute (serverless)
  - EKS: Running ECS on AWS-powered Kubernetes (running on EC2)
  - ECR: Docker Container Registry hosted by AWS
- ECS & Docker are very popular for microservices
- **For now, for the exam, only “ECS Core” & ECR is in scope**
- IAM security and roles at the ECS task level

### What’s Docker?
- Docker is a “container technology”
- Run a containerized application on any machine with Docker installed
- Containers allows our application to work the same way anywhere
- Containers are isolated from each other
- Control how much memory / CPU is allocated to your container
- Ability to restrict network rules
- More efficient than Virtual machines
- Scale containers up and down very quickly (seconds)

### AWS ECS – Use cases
- Run microservices
- Ability to run multiple docker containers on the same machine
- Easy service discovery features to enhance communication
- Direct integration with Application Load Balancers
- Auto scaling capability
- Run batch processing / scheduled tasks
- Schedule ECS containers to run on On-demand / Reserved / Spot instances
- Migrate applications to the cloud
- Dockerize legacy applications running on premise
- Move Docker containers to run on ECS

[*]
### AWS ECS – ALB integration
- Application Load Balancer (ALB) has a direct integration feature with ECS called “port mapping”
- This allows you to run multiple instances of the same application on the same EC2 machine
- Use cases:
  - Increased resiliency even if runningon one EC2 instance
  - Maximize utilization of CPU / cores
  - Ability to perform rolling upgrades without impacting application uptime

### AWS ECS – ECS Setup & Config file
- Run an EC2 instance, install the ECS agent with ECS config file
- Or use an ECS-ready Linux AMI (still need to modify config file)

- ECS Config file is at **/etc/ecs/ecs.config**
ECS_CLUSTER=
ECS_ENGINE_AUTH_dATA=
ECS_AVAILABLE_LOGGING_DRIVERS=
ECS_ENABLE_TASK_IAM_ROLE=true

[SAA-C02]
### ECS - IAM Task Roles
- The EC2 instance should have an IAM role allowing it to access the ECS service (for the ECS agent)
- Each ECS task should have an ECS IAM task role to perform their API calls
- Use the “taskRoleArn” parameter in a task definition

[SAA-C02]
### Fargate
• When launching an ECS Cluster, we have to create our EC2 instances
• If we need to scale, we need to add EC2 instances
• So we manage infrastructure…

• With Fargate, it’s all Serverless!
• We don’t provision EC2 instances
• We just create task definitions, and AWS will run our containers for us
• To scale, just increase the task number. Simple! No more EC2 J

[SAA-C02]
### Amazon EKS Overview
• Amazon EKS standards for Amazon Elastic **Kubernetes** Service
• It is a way to launch **managed Kubernetes clusters on AWS**
• Kubernetes is an open-source system for automatic deployment, scaling
and management of containerized (usually Docker) application
• It’s an alternative to ECS, similar goal but different API
• EKS supports **EC2** if you want to to deploy worker nodes or **Fargate** to
deploy serverless containers
• **Use case**: if your company is already using Kubernetes on-premises or in
another cloud, and wants to migrate to AWS using Kubernetes

### AWS Step Functions
• Build serverless visual workflow to orchestrate your Lambda functions
• Represent flow as a JSON state machine
• Features: sequence, parallel, conditions, timeouts, error handling…
• Can also integrate with EC2, ECS, On premise servers, API Gateway
• Maximum execution time of 1 year
• Possibility to implement human approval feature
• Use cases:
  • Order fulfillment
  • Data processing
  • Web applications
  • Any workflow

### Quick word on Chef / Puppet
• They help with managing configuration as code
• Helps in having consistent deployments
• Works with Linux / Windows
• Can automate: user accounts, cron, ntp, packages, services…

• They leverage “Recipes” or ”Manifests”

• Chef / Puppet have similarities with SSM / Beanstalk / CloudFormation
but they’re open-source tools that work cross-cloud

------

## Other Services: Cheat Sheet

Here's a quick cheat-sheet to remember all these services:

**CodeCommit**: service where you can store your code. Similar service is GitHub

**CodeBuild**: build and testing service in your CICD pipelines

**CodeDeploy**: deploy the packaged code onto EC2 and AWS Lambda

**CodePipeline**: orchestrate the actions of your CICD pipelines (build stages, manual approvals, many deploys, etc)

**CloudFormation**: Infrastructure as Code for AWS. Declarative way to manage, create and update resources.

**ECS** (Elastic Container Service): Docker container management system on AWS. Helps with creating micro-services.

**ECR** (Elastic Container Registry): Docker images repository on AWS. Docker Images can be pushed and pulled from there

**Step Functions**: Orchestrate / Coordinate Lambda functions and ECS containers into a workflow

**SWF** (Simple Workflow Service): Old way of orchestrating a big workflow.

**EMR** (Elastic Map Reduce): Big Data / Hadoop / Spark clusters on AWS, deployed on EC2 for you

**Glue**: ETL (Extract Transform Load) service on AWS

**OpsWorks**: managed Chef & Puppet on AWS

**ElasticTranscoder**: managed media (video, music) converter service into various optimized formats

**Organizations**: hierarchy and centralized management of multiple AWS accounts

**Workspaces**: Virtual Desktop on Demand in the Cloud. Replaces traditional on-premise VDI infrastructure

**AppSync**: GraphQL as a service on AWS

**SSO** (Single Sign On): One login managed by AWS to log in to various business SAML 2.0-compatible applications (office 365 etc)

------

Other Services: Quiz

Quiz 23|16 questions

Question 1:
You are looking for a service to store docker images in AWS. Which one do you recommend?
A: ECR

  Amazon Elastic Container Registry (ECR) is a fully-managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker containers

Question 2:
You would like to find a managed-service in AWS alternative to GitLab, in order to version control your code entirely in AWS. Which technology do you recommend?
A: CodeCommit

  CodeCommit is used to store and version control your code and as such, it's an alternative to GitLab and GitHub


Question 3:
As part of your disaster recovery strategy, you would like to make sure your entire infrastructure is code, so that you can easily re-deploy it in any region. Which service do you recommend?
A: CloudFormation

  CloudFormation is the de-facto service in AWS for infrastructure as code.

Question 4:
You need to manage a fleet of Docker containers in the cloud, which service do you recommend?
A: ECS

  ECS is a container orchestrator service and the correct service to manage a fleet of Docker containers in the cloud

Question 5:
You would like to orchestrate your CICD pipeline to deliver all the way to Elastic Beanstalk. Which service do you recommend?
A: CodePipeline

  CodePipeline is a CICD orchestration service, and has an integration with Elastic Beanstalk

Question 6:
You need to deploy your code to a fleet of EC2 instances with a specific strategy. Which technology do you recommend?
A: CodeDeploy

  When deploying code directly onto EC2 instances or On Premise servers, CodeDeploy is the service to use. You can define the strategy (how fast the rollout of the new code should be)

Question 7:
You have a Jenkins CI build server hosted on premise and you would like to de-commission it and replace it by a managed service on AWS. Which service do you recommend?
A: CodeBuild

  CodeBuild is an alternative to Jenkins

Question 8:
You need to orchestrate a series of AWS Lambda function into a workflow. Which service do you recommend?
A: Step Functions

Question 9:
You are looking to create an Hadoop cluster to perform Big Data Analysis. Which service do you recommend on using?
A: EMR (Elastic MapReduce)

  EMR is the AWS way of creating an Hadoop cluster with the tools of your choosing.

Question 10:
You are looking to move data all around your AWS databases using a managed ETL service that has a metadata catalog feature. Which one do you recommend?
A: Glue

  Glue is an ETL service

Question 11:
Your company is already using Chef recipes to manage its infrastructure. You would like to move to the AWS cloud and keep on using Chef. What service do you recommend?
A: OpsWorks

Question 12:
You work for a consulting company which has recently decided to create video training content for their clients. They would like to view the videos on different devices such as iPhone, iPad, Web browsers. Which service do you recommend to convert the videos?
A: Elastic Transcoder

Question 13:
Your organization would like to create various accounts to physically separate their dev, test and production environments. Your IT lead would still like to manage these environments centrally from a billing purposes, in order for management to be simple. Which service do you recommend?
A: Organizations

  AWS Organizations allow you to create multiple AWS accounts and centralize them around a single organization for simplified and unified billing.

Question 14:
You have a VDI (Virtual Desktop Infrastructure) on premise and as a solution architect, you would like to optimize maintenance and management cost by switching to virtual desktops on the AWS Cloud. Which service do you recommend?
A: Workspaces

  Amazon WorkSpaces is a managed, secure cloud desktop service. You can use Amazon WorkSpaces to provision either Windows or Linux desktops

Question 15:
Your developers are creating a mobile application and would like to have a managed GraphQL backend. Which service do you recommend?
A: AppSync

Question 16:
You are deploying your application on an ECS cluster made of EC2 instances. The cluster is hosting one application that has been issuing API calls to DynamoDB successfully. Upon adding a second application, which issues API calls to S3, you are getting authorization issues. What should you do to resolve the problem and ensure proper security?
A: Create an IAM task role for the new application

------

## Section 25: WhitePapers and Architectures - AWS Certified Solutions Architect Associate


### Well Architected Framework General Guiding Principles
• Stop guessing your capacity needs
• Test systems at production scale
• Automate to make architectural experimentation easier
• Allow for evolutionary architectures
• Design based on changing requirements
• Drive architectures using data
• Improve through game days
• Simulate applications for flash sale days

## Well Architected Framework
5 Pillars
• 1) Operational Excellence
• 2) Security
• 3) Reliability
• 4) Performance Efficiency
• 5) Cost Optimization
• They are not something to balance, or trade-offs, they’re a synergy

## Well Architected Framework
• It’s also questions!
• Let’s look into the Well-Architected Tool
• https://console.aws.amazon.com/wellarchitected AWS Well-Architected Tool

## 1) Operational Excellence
• Includes the ability to run and monitor systems to deliver business value
and to continually improve supporting processes and procedures
• Design Principles
  • Perform operations as code - Infrastructure as code
  • Annotate documentation - Automate the creation of annotated documentation
  after every build
  • Make frequent, small, reversible changes - So that in case of any failure, you can reverse it
  • Refine operations procedures frequently - And ensure that team members are
  familiar with it
  • Anticipate failure
  • Learn from all operational failures

------

WhitePaper Quiz
Quiz 24|1 question

Question 1:
You would like to get AWS recommendations on actual potential cost savings, performance, service limits improvements amongst other things. Which service do you recommend?
A: Trusted Advisor

------

------

aws configure --profile

aws configure set default.s3.signature_version s3v4

Not working
* Lecture 100

-----

UTILS UTLS

## AWS Policy Generator
https://awspolicygen.s3.amazonaws.com/policygen.html
