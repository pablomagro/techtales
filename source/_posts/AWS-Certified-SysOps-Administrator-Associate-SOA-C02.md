---
title: AWS Certified SysOps Administrator – Associate (SOA-C02)
date: 2023-05-15 13:27:03
tags:
  - Certifications
  - SysOps
  - SOA-C02
categories:
  - AWS
---

## CloudWatch

### Alarms
CloudWatch alarms allow you to monitor metrics and trigger actions based on defined thresholds. In this case, you can create a CloudWatch alarm that monitors the CPU utilization metric of the EC2 instance. When the CPU utilization reaches 100%, the alarm will be triggered, and you can configure actions such as sending notifications or executing automated actions to address the unresponsiveness issue.

### For each production EC2 instance, create an Amazon CloudWatch alarm for Status Check Failed: System. Set the alarm action to recover the EC2 instance. Configure the alarm notification to be published to an Amazon Simple Notification Service (Amazon SNS) topic.

``Explanation``: By creating a `CloudWatch alarm` for Status Check Failed: System, you can` automate the recovery task of EC2 instances` (stop, terminate,
reboot, or recover your Amazon EC2 instances). When the system health check fails for an EC2 instance, the alarm will be triggered and perform the configured action to recover the instance. This eliminates the need for manual intervention. Additionally, configuring the alarm to publish notifications to an SNS topic allows you to receive notifications whenever a system health check fails.

### Metrics

#### Determine which instance use the most bandwidth
``NetworkIn`` ``and NetworkOut``

#### Identify the processing power required
``CPUUtilization`` specifies the percentage of allocated EC2 compute units that are currently in use on the instance. This metric identifies the processing power required to run an application on a selected instance. This metric is expressed in Percent.

#### Number of users.
``ActiveConnectionCount`` This metric `represents` the `total number of concurrent TCP connections active` from clients to the load balancer and from the load balancer to targets.

#### RAMUtilization is `NOT available as` an `EC2 metric`
``RAMUtilization`` You can publish your own metrics to CloudWatch using the AWS CLI or an API. You can view statistical graphs of your published metrics with the AWS Management Console. Metrics produced by AWS services are standard resolution by default.

#### 5xx server errors
To monitor the number of 500 Internal Error responses that you're getting, you can enable Amazon CloudWatch metrics. Amazon S3 CloudWatch request metrics include a metric for 5xx server errors.

#### `*Q` 4xxx
You can set an alarm to notify operators when the 404 filter metric exceeds a threshold.

#### Events
You can run `CloudWatch Events` rules according to a `schedule`.

#### EBS Snapshots
It is possible to `create an automated snapshot of an existing Amazon Elastic Block Store (Amazon EBS)` volume on a schedule. You can choose a fixed rate to create a snapshot every few minutes or use a cron expression to specify that the snapshot is made at a specific time of day.

Snapshots are incremental backups, which means that only the blocks on the device that have changed after your most recent snapshot are saved. This minimizes the time required to create the snapshot and saves on storage costs by not duplicating data. Each snapshot contains all of the information that is needed to restore your data (from the moment when the snapshot was taken) to a new EBS volume.

Reference: [Schedule Automated Amazon EBS Snapshots Using CloudWatch Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/TakeScheduledSnapshot.html)

### *Q [Filters](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/MonitoringLogData.html)
You can create a `count` of `404` errors `and exclude` other `4xx` errors with a filter pattern on 404 errors.

### Agents

#### Custom Metrics
You can retrieve custom metrics from your applications or services using the `StatsD` and `collectd` protocols. StatsD is supported on both Linux servers and servers running Windows Server. collectd is supported only on Linux

#### Install Agents to track the state of each of the instances
You must attach the ``CloudWatchAgentServerRole`` IAM role to the EC2 instance to be able to run the CloudWatch agent on the instance. This role enables the CloudWatch agent to perform actions on the instance.

### Instal CloudWatch agent
If your AMI contains a CloudWatch agent, it’s automatically installed on EC2 instances when you create an EC2 Auto Scaling group. With the stock Amazon Linux AMI, you need to install it (AWS recommends to install via yum).

### CloudWatch Synthetics
CloudWatch Synthetics canaries are automated scripts that monitor the availability and performance of applications, endpoints, and APIs. They are `designed to simulate user interactions with an application and provide insights into its behavior`.

Canaries are created using scripts written in Node.js or Python and are scheduled to run at regular intervals. These scripts perform tasks such as navigating through a website, clicking on specific elements, submitting forms, and validating responses. By executing these predefined actions, canaries can monitor the functionality, responsiveness, and performance of an application or API.

CloudWatch Synthetics canaries collect data on metrics like response time, latency, availability, and success rates. They can also be configured to generate alarms when certain conditions are met, allowing proactive identification and remediation of issues.

#### Reference
[https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor-check-reference.html](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor-check-reference.html)

## CloudTrail

### Q. To ensure that SysOps administrators can easily verify that the CloudTrail log files have not been deleted or changed, the following action should be taken:
Enable `CloudTrail log file integrity validation` when the trail is created or updated.

``Explanation``: Enabling `CloudTrail log file integrity validation` ensures that the log files are protected against tampering or unauthorized modification. CloudTrail uses SHA-256 hashes to validate the integrity of the log files stored in Amazon S3. By enabling this feature, the SysOps administrators can easily verify the integrity of the log files and ensure that they have not been deleted or changed.

## `*Q` [AWS Artifact](https://docs.aws.amazon.com/artifact/latest/ug/what-is-aws-artifact.html)
AWS Artifact `keeps compliance-related reports and agreements`.

## `*Q` AWS Config
AWS Config `keeps track of` the `configuration` of `your AWS resources and their relationships to other resources`. It can also `evaluate` those AWS `resources for compliance`. This service uses rules that can be configured to evaluate AWS resources against desired configurations. E.g. can track `changes` to `CloudFormation stacks`.

## `*Q` [AWS Inspector](https://aws.amazon.com/inspector/)
Amazon Inspector is `used for security compliance of instances and applications`.

Amazon Inspector is an automated security assessment service that helps you `test` the `network accessibility` of your Amazon EC2 instances and the `security state of your applications running on the instances`.

An Amazon Inspector assessment report can be generated for an assessment run once it has been successfully completed. An assessment report is a document that details what is tested in the assessment run, and the results of the assessment. The results of your assessment are formatted into a standard report, which can be generated to share results within your team for remediation actions, to enrich compliance audit data, or to store for future reference.

You can select from two types of report for your assessment, a findings report or a full report. The findings report contains an executive summary of the assessment, the instances targeted, the rules packages tested, the rules that generated findings, and detailed information about each of these rules along with the list of instances that failed the check. The full report contains all the
information in the findings report and additionally provides the list of rules that were checked and passed on all instances in the assessment target.

## `*Q` [AWS Trusted Advisor](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor.html)
Trusted Advisor provides real-time guidance to help users follow AWS best practices to provision their resources

E.g. AWS Trusted Advisor checks for service `usage` that is more than 80% of the `service limit`.

### Check categories
- Cost optimization
- Performance
- Security
- Fault tolerance
- Service limits


### AWS Config Auto Remediation
Has auto remediate feature for any non-compliant S3 buckets using the following AWS Config rules:

s3-bucket-logging-enabled s3-bucket-server-side-encryption-enabled s3-bucket-public-read-prohibited s3-bucket-public-write-prohibited

These AWS Config rules act as controls to prevent any non-compliant S3 activities.

## Memcached

### Fix high Memcached evictions
To fix the issue of high Memcached evictions in Amazon ElastiCache, the following actions should be taken:

1. `Increase` the `size of the nodes` in the cluster: This allows for more available memory in each node, reducing the likelihood of evictions due to limited cache space.
1. `Increase` the `number of nodes` in the cluster: By adding more nodes, the overall cache capacity increases, reducing the chance of evictions.

The [Evictions metric](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/CacheMetrics.WhichShouldIMonitor.html#metrics-evictions) for Amazon ElastiCache for Memcached represents the number of nonexpired items that the cache evicted to provide space for new items. If you are experiencing evictions with your cluster, it is usually a sign that you need to scale up (use a node that has a larger memory footprint)
or scale out (add additional nodes to the cluster) to accommodate the additional data

## [VPC](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html#what-is-privatelink)
With Amazon Virtual Private Cloud (Amazon VPC), you can launch AWS resources in a logically isolated virtual network that you've defined. This virtual network closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of AWS.

### Configuration
`Regardless of the type of subnet, the internal IPv4 address range of the subnet is always private`. AWS never announces these address blocks to the internet.

`When you create a VPC, you must specify a range of IPv4 addresses for the VPC` in the form of a Classless Inter-Domain Routing (CIDR) block; for example, 10.0.0.0/16. This is the primary CIDR block for your VPC.

`Subnets created in a VPC can communicate with each other`, this is default behaviour. The main route table facilitates this communication.

Reference: [How Amazon VPC works](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html)

### Connect the Lambda function to a private subnet that has a route to a NAT gateway deployed in a public subnet of the VPC.
``Explanation``: By connecting the Lambda function to a private subnet with a route to a NAT gateway, the function can access resources within the VPC while also leveraging the NAT gateway to access the internet and communicate with third-party APIs. The NAT gateway acts as a bridge between the private subnet and the internet, allowing the Lambda function to securely access external resources.

### VPC Endpoint
A VPC Endpoint allows you to `connect` your `VPC` directly `to AWS services` without the need for `internet gateways`, `NAT gateways`, or `VPN connections`. It enables private communication between your VPC and the AWS service without going over the internet.

To configure a VPC Endpoint for accessing AWS Systems Manager APIs, you can follow these steps:

1. Create a VPC Endpoint for AWS Systems Manager in your Amazon VPC. This creates an elastic network interface with a private IP address within your VPC.
1. Update the route tables in your VPC to route traffic destined for the AWS Systems Manager API endpoints to the VPC Endpoint. This ensures that traffic is directed through the VPC Endpoint instead of going over the internet.
1. Verify that your on-premises instances and AWS managed instances are configured to use the appropriate VPC and route tables.

### Egress-only Internet Gateway
An egress-only internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows outbound communication over IPv6 from instances in your VPC to the internet, and prevents the internet from initiating an IPv6 connection with your instances.

An egress-only internet gateway is for use with `IPv6 traffic only`. To enable outbound-only internet communication `over IPv4`, use a `NAT gateway` instead.

Reference: [Enable outbound IPv6 traffic using an egress-only internet gateway](https://docs.aws.amazon.com/vpc/latest/userguide/egress-only-internet-gateway.html)

### Carrier gateway
A Carrier gateway is a highly available virtual appliance that ``provides outbound IPv6 internet connectivity for instances in your VPC``. It acts as a gateway between your VPC and the internet, `allowing` IPv6 `traffic` to flow `in and out` of your `VPC`. By configuring a Carrier gateway, you can enable outbound communication over IPv6 for the EC2 instances in the private subnets while keeping them isolated from direct internet access.

## Security Group

### The reason for the issue where the new EC2 instances are unable to mount the Amazon EFS file system in a new Availability Zone could be:
The security group for the mount target does not allow inbound NFS connections from the security group used by the EC2 instances.

``Explanation``: When mounting an Amazon EFS file system from EC2 instances, the security group associated with the mount target should allow inbound NFS (Network File System) connections from the security group used by the EC2 instances. By default, the security group associated with the mount target allows inbound connections from the default security group of the VPC. If the EC2 instances are using a different security group, it needs to be added to the mount target's security group's inbound rules to allow NFS connections.

## CloudFormation

### StackSets

#### `Use` AWS CloudFormation `StackSets for Multiple Accounts in an AWS Organization`:
Use AWS CloudFormation `StackSets` to `deploy a template` to `each account` to create the new IAM roles.

``Explanation``: AWS CloudFormation StackSets allows you to deploy a CloudFormation template across multiple AWS accounts. By using StackSets, you can create and manage the same IAM roles in each account within the organization. This ensures consistent deployment of roles across accounts and simplifies the management process.

``Reference``: [New: Use AWS CloudFormation StackSets for Multiple Accounts in an AWS Organization](https://aws.amazon.com/blogs/aws/new-use-aws-cloudformation-stacksets-for-multiple-accounts-in-an-aws-organization/)

### `*Q` [AutoScalingRollingUpdate policy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-attribute-updatepolicy.html)
With rolling updates, you can specify whether CloudFormation performs updates in batches or all at once for instances that are in an Auto Scaling group. The `AutoScalingRollingUpdate` policy is the only CloudFormation feature that provides such an incremental update throughout the Auto Scaling group.

### `*Q` To lunch the last AMI.
Use the Parameters section in the template to specify the Systems Manager (SSM) Parameter, which contains the latest version of the Windows regional AMI ID.

```YAML
Parameters:
  LatestWindowsAMIParameter:
    Type: AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
    Default: /LatestWindowsAMI


Parameters:
  LatestWindowsAMIParameter:
    Type: AWS::SSM::Parameter::Value<AWS::EC2::Image::Id>
    Default: /LatestWindowsAMI
```

### `*Q` `UpdatePolicy` attribute
By adding the `UpdatePolicy` attribute in CloudFormation and enabling the WaitOnResourceSignals property, the Auto Scaling group update process will be handled more gracefully. This approach allows CloudFormation to monitor the health and success of each instance during the update process before moving on to the next instance.

Appending a health check at the end of the user data script allows the instance to signal CloudFormation that it has successfully completed its initialization. This helps ensure that the instance is fully operational before proceeding to the next instance in the Auto Scaling group update process.

## AWS Backup

### For the production account, a SysOps administrator must ensure that all data is backed up daily for all current and future Amazon EC2 instances and Amazon Elastic File System (Amazon EFS) file systems. Backups must be retained for 30 days
Create a backup plan in AWS Backup. Assign resources by resource ID, selecting all existing EC2 and EFS resources that are running in the account. Edit the backup plan daily to include any new resources. Schedule the backup plan to run every day with a lifecycle policy to expire backups after 30 days.

``Explanation``: AWS Backup provides a centralized and automated solution for backing up data. By creating a backup plan and assigning resources by resource ID, you can easily include all existing EC2 instances and EFS file systems in the backup process. Editing the backup plan daily ensures that any new resources are automatically included in the backups. By scheduling the backup plan to run every day and configuring a lifecycle policy to expire backups after 30 days, you meet the requirement of daily backups with a retention period of 30 days.

## EBS

### Q. To set up a backup strategy for an Amazon Elastic Block Store (Amazon EBS) volume storing a custom database on an Amazon EC2 instance, the following action should be taken:
Create an Amazon `Data Lifecycle Manager (Amazon DLM)` policy to `take` a `snapshot of the EBS` volume on a `recurring schedule`.

``Explanation``: Amazon Data Lifecycle Manager (Amazon DLM) allows you to create automated snapshot lifecycle policies for your Amazon EBS volumes. By creating an Amazon DLM policy, you can define the desired backup schedule and retention period for the EBS volume. The policy will then automatically create snapshots according to the defined schedule. This ensures that regular backups are taken and can be used for data recovery if needed.

### EBS volumes deleted with the `TerminateInstances` API call continue to show for some time on AWS Config console
Terminated Amazon EC2 instances use the ``DeleteOnTermination`` attribute for each attached EBS volume to determine to delete the volume. Amazon EC2 deletes the Amazon EBS volume that has the ``DeleteOnTermination`` attribute set to true, but it does not publish the ``DeleteVolume`` API call. This is because AWS Config uses the DeleteVolume API call as a trigger with the rule, and the resource changes aren't recorded for the EBS volume. The EBS volume still shows as compliant or noncompliant.

AWS Config performs a baseline every six hours to check for new configuration items with the ResourceDeleted status. The AWS Config rule then removes the deleted EBS volumes from the evaluation results.

### SSD-backed volumes (IOPS-intensive)

## Provisioned IOPS SSD (io2 Block Express, io2 & `io1`) volumes
Provisioned IOPS SSD volumes are designed to deliver a maximum of 256,000 IOPS, 4,000 MB/s of throughput, and 64 TiB in size per volume1. io2 Block Express is the latest generation of the Provisioned IOPS SSD volumes that delivers 4x higher throughput, IOPS, and capacity than regular io2 volumes, along with sub-millisecond latency – at the same price as io2. io2 Block Express provides highest block storage performance for the largest, most I/O- intensive, mission-critical deployments of Oracle, Microsoft SQL Server, SAP HANA, and SAS Analytics

#### General purpose SSD (``gp3 and gp2``) volumes
General-purpose volumes are backed by solid-state drives (SSDs) and are suitable for a broad range of transactional workloads, virtual desktops, medium sized single instance databases, latency sensitive interactive applications, dev/test environments, and boot volumes.

### HDD-backed volumes (MB/s-intensive)

### Throughput optimized HDD (``st1``) volumes
ST1 is backed by hard disk drives (HDDs) and is ideal for frequently accessed, throughput intensive workloads with large datasets and large I/O sizes, such as MapReduce, Kafka, log processing, data warehouse, and ETL workloads.

### Cold HDD (``sc1``) volumes
SC1 is backed by hard disk drives (HDDs) and provides the lowest cost per GB of all EBS volume types. It is ideal for less frequently accessed workloads with large, cold datasets.

### Changing the instance type
1. The possibility to resize an instance depends on whether the root device is an EBS volume. If it is, you can easily change the instance size by modifying its instance type, also known as resizing. However, if the root device is an instance store volume, you need to migrate your application to a new instance with the desired instance type.
2. Before changing the instance type of your Amazon EBS-backed instance, you must stop it. AWS will then move the instance to new hardware, but the instance ID will remain the same.
3. If your instance belongs to an Auto Scaling group, the Amazon EC2 Auto Scaling service considers the stopped instance as unhealthy and may terminate it, launching a replacement instance instead. To avoid this, you can temporarily suspend the scaling processes for the group while resizing your instance.

Reference: [Amazon EBS features](https://aws.amazon.com/ebs/features/)

## S3

### Retain Until Date
A retention period safeguards an object version for a specified duration. When a retention period is assigned to an object version, Amazon S3 records a timestamp in the object version's metadata, indicating when the retention period concludes. Once the retention period ends, the object version can be overwritten or deleted, unless a legal hold has also been placed on it.

You can assign a retention period to an object version either explicitly or through a default setting at the bucket level. Explicitly applying a retention period involves specifying a "Retain Until Date" for the object version. Amazon S3 stores this setting in the object version's metadata and ensures the protection of the object version until the retention period expires.

#### References
1. [https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lock.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lock.html)
1. [https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lock-overview.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lock-overview.html)
1. [https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html)

### S3 RTC S3 (Replication Time Control)
S3 Replication Time Control (S3 RTC) helps you meet compliance or business requirements for data replication and provides visibility into Amazon S3 replication times. S3 RTC replicates most objects that you upload to Amazon S3 in seconds, and 99.99 percent of those objects within 15 minutes.

Reference: [Using S3 Replication Time Control](https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication-time-control.html#using-s3-events-to-track-rtc)

## Amazon S3 Access Points
Allow you to `create unique entry points for accessing your S3 buckets`. Each access point can have its own access policy, allowing you to control access at a granular level. By using access points, you can assign specific permissions to each application or team accessing the shared bucket without affecting other applications. This helps in maintaining access control and minimizing the risk of unintended changes to the bucket policy.

Reference: [Amazon S3 Access Points](https://aws.amazon.com/s3/features/access-points/)

### Logs

#### S3 Server Access Logging
To `track requests for access to your bucket`, you can enable server access logging. Each access log record provides details about a single access request, such as the requester, bucket name, request time, request action, response status, and an error code, if relevant.

There is no extra charge for enabling server access logging on an Amazon S3 bucket, and you are not charged when the logs are PUT to your bucket. However, any log files that the system delivers to your bucket accrue the usual charges for storage. You can delete these log files at any time. Subsequent reads and other requests to these log files are charged normally, as for any other object, including data transfer charges.

By default, logging is disabled. When logging is enabled, logs are saved to a bucket in the same AWS Region as the source bucket.

Reference: [Using Amazon S3 access logs to identify requests](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-s3-access-logs-to-identify-requests.html)

### As a Website
If you use an Amazon S3 bucket configured as a website endpoint, ``you must set it up with CloudFront as a custom origin``. You can’t use the origin access identity feature. However, you can restrict access to content on a custom origin by setting up custom headers and configuring your origin to require them.

### [Enable MFA-Delete](https://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html#MultiFactorAuthenticationDelete)
You should note that `only` the bucket owner (`root account`) `can enable MFA Delete` only `via` the AWS `CLI`. However, the bucket owner, the AWS account that created the bucket (root account), and all authorized IAM users can enable versioning.

### Vault Lock Policy
S3 Glacier Vault Lock `allows` you to easily deploy and `enforce compliance controls for individual S3 Glacier vaults` with a `vault lock policy`. You `can specify controls` such as `“write once read many” (WORM)` in a vault lock policy and lock the policy from future edits. Once locked, the policy can no longer be changed.

### `*Q` Snowball Edge
AWS Snowball is a service designed for large-scale data transfers. Snowball Edge appliances are rugged, petabyte-scale data transfer devices that can be used for offline data migration. By using multiple instances of the AWS Snowball client and multiple Snowball Edge Appliances, the company can achieve fast and cost-effective data migration.

Using multiple instances of the AWS Snowball client and Snowball Edge Appliances `allows` for `parallel data transfers`, significantly `reducing the migration time`. It also `avoids` the need for `network-based transfers`, which could be slower and potentially costly due to data transfer charges.

## [Amazon S3 Storage Classes](https://aws.amazon.com/s3/storage-classes/)

### Amazon S3 Standard-Infrequent Access (S3 Standard-IA)
S3 Standard-IA is for data that is accessed less frequently, but requires rapid access when needed. S3 Standard-IA offers the high durability, high throughput, and low latency of S3 Standard, with a low per GB storage price and per GB retrieval charge.


## [AWS OpsHub](https://docs.aws.amazon.com/snowball/latest/developer-guide/aws-opshub.html)
AWS OpsHub for `Snow Family`, that you can use to `manage your devices and local AWS services`. You use AWS OpsHub on a client computer to perform tasks such as unlocking and configuring single or clustered devices, transferring files, and launching and managing instances running on Snow Family Devices. You can use AWS OpsHub to manage both the Storage Optimized and Compute Optimized device types and the Snow device. The AWS OpsHub application is available at no additional cost to you.

AWS OpsHub takes all the existing operations available in the Snowball API and presents them as a graphical user interface. This interface helps you quickly migrate data to the AWS Cloud and deploy edge computing applications on Snow Family Devices.

When your Snow device arrives at your site, you download, install, and launch the AWS OpsHub application on a client machine, such as a laptop. After installation, you can unlock the device and start managing it and using supported AWS services locally. AWS OpsHub provides a dashboard that summarizes key metrics such as storage capacity and active instances on your device. It also provides a selection of AWS services that are supported on the Snow Family Devices. Within minutes, you can begin transferring files to the device.

## IAM

### If an IAM user, with full access to IAM and Amazon S3, assigns a bucket policy to an Amazon S3 bucket and doesn't specify the AWS account root user as a principal, the root user is denied access to that bucket.
To fix this issue, the CTO needs to ensure that an IAM user with full access to both IAM and Amazon S3 explicitly includes the AWS account root user as a principal in the bucket policy of the S3 bucket. By adding the root user as a principal, access will be granted to the CTO and they will be able to access the S3 bucket in their AWS account.

### Reference:
[https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_iam-s3.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_iam-s3.html)

### IAM Policy Types
You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources. A policy is an object in AWS that, when associated with an identity or resource, defines their permissions. Resource-based policies are JSON policy documents that you attach to a resource such as an Amazon S3 bucket. These policies grant the specified principal permission to perform specific actions on that resource and define under what conditions this applies.

- ``Identity-based`` policies are attached to an IAM user, group, or role. These policies let you specify what that identity can do (its permissions).
- ``Resource-based`` policies are attached to a resource. For example, you can attach resource-based policies to Amazon S3 buckets, Amazon SQS queues, and AWS Key Management Service encryption keys.
- ``Identity-based`` policies and ``resource-based`` policies are both permissions policies and are evaluated together. For a request to which only permissions policies apply, AWS first checks all policies for a Deny. If one exists, then the request is denied. Then AWS checks for each Allow. If at least one policy statement allows the action in the request, the request is allowed. It doesn't matter whether the Allow is in the identity-based policy or the resource-based policy.

#### Trust policy
Defines which principal entities (accounts, users, roles, and federated users) can assume the role. An IAM role is both an identity and a resource that supports resource-based policies. For this reason, you `must attach both a trust policy and an identity-based policy to an IAM role`. The `IAM service` `supports only one` type of `resource-based` policy called a `role trust policy`, which is attached to an IAM role.

References: [Identity-based policies and resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html)

## ELB

### [Elastic Load Balancing and AWS X-Ray](https://docs.aws.amazon.com/xray/latest/devguide/xray-services-elb.html)
Elastic Load Balancing application load balancers add a trace ID to incoming HTTP requests in a header named X-Amzn-Trace-Id.

      X-Amzn-Trace-Id: Root=1-5759e988-bd862e3fe1be46a994272793

`Load balancers do not send data to X-Ray`, and do not appear as a node on your service map.

### ELB access logs
ELB access logs is an optional feature of Elastic Load Balancing that is disabled by default. The access logs capture detailed information about requests sent to your load balancer. Each log contains information such as the time the request was received, the client's IP address, latencies, request paths, and server responses. You can use these access logs to analyze traffic patterns and troubleshoot issues. Each access log file is automatically encrypted using SSE-S3 before it is stored in your S3 bucket and decrypted when you access it. You do not need to take any action; the encryption and decryption is performed transparently

Reference: [Access logs for your Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-access-logs.html)

### CloudTrail logs
`Elastic Load Balancing` is `integrated` with `AWS CloudTrail`, a service that provides a record of actions taken by a user, role, or an AWS service in Elastic Load Balancing. `CloudTrail captures` all `API calls for Elastic Load Balancing as events`. The calls captured include calls from the AWS Management Console and code calls to the Elastic Load Balancing API operations.

## Amazon Machine Images (AMIs)

### Sharing
The key points to consider before planning the expansion and sharing of Amazon Machine Images (AMIs) are:

1. AMIs are regional resources and can be shared across Regions: AMIs are specific to a particular AWS Region. If you want to use an AMI in a different Region, you need to copy the AMI to that Region. Sharing an AMI across Regions requires creating a new copy in each desired Region.
2/ You need to share any CMKs used to encrypt snapshots and any Amazon EBS snapshots that the AMI references: If the AMI references Amazon Elastic Block Store (EBS) snapshots, you must also share those snapshots. Additionally, if the snapshots are encrypted using customer-managed customer master keys (CMKs), you need to share the CMKs as well.

## EC2

### Errors
#### ``Client.InternalError: Client error on launch``
1. error is caused when an Auto Scaling group attempts to launch an instance that has an encrypted EBS volume, but the service-linked role does not have access to the customer-managed CMK used to encrypt it. Additional setup is required to allow the Auto Scaling group to launch instances.

### Termination Policy
1. You `can't enable termination protection for Spot Instances`, a Spot Instance is terminated when the Spot price exceeds the amount you're willing to pay for Spot Instances. However, you can prepare your application to handle Spot Instance interruptions.
1. To prevent instances that are part of an Auto Scaling group from terminating on scale in, use instance protection. The `DisableApiTermination` attribute does not prevent Amazon EC2 Auto Scaling from terminating an instance.

### Spot Instances Interruptions
You can specify that Amazon EC2 should do one of the following when it interrupts a Spot Instance:

1. ``Stop`` the Spot Instance
1. ``Hibernate`` the Spot Instance
1. ``Terminate`` the Spot Instance

The default is to `terminate` Spot Instances when they are interrupted.

### `*Q` [Spot Fleet Config Cost Optimization](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/how-spot-fleet-works.html)
Using `lowestPrice` allocation `strategy` a Spot Fleet automatically deploys the lowest price combination of instance types and Availability Zones based on the current Spot price across the number of Spot pools specified. You can use this combination to avoid the most expensive Spot Instances.

### Recover impaired instances
A Systems Manager Automation document defines the Automation workflow (the actions that Systems Manager performs on your managed instances and AWS resources). Automation includes several pre-defined Automation documents that you can use to perform common tasks like restarting one or more EC2 instances or creating an Amazon Machine Image (AMI).

Use the ``AWSSupport-ExecuteEC2Rescue`` document to recover impaired instances.

### `*Q` Get public IP address
EC2 instances in AWS have `metadata` associated with them that can be accessed from within the instance. This metadata includes information about the instance, such as its IP address, instance type, security groups, and more.

Can make an HTTP GET request to a specific URL provided by the instance metadata service. The URL is http://169.254.169.254/latest/meta-data/public-ipv4.

## Detailed monitoring
`Metrics are the fundamental concept in CloudWatch`. A metric represents a time-ordered set of data points that are published to CloudWatch. Think of a metric as a variable to monitor, and the data points as representing the values of that variable over time.

`By default, your instance is enabled for basic monitoring`. You can optionally enable detailed monitoring. After you enable detailed monitoring, the Amazon EC2 console displays monitoring graphs with a 1-minute period for the instance.

Reference: [Enable or turn off detailed monitoring for your instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-cloudwatch-new.html)

## AWS Storage Gateway
AWS Storage Gateway is a set of hybrid cloud storage services that provide on-premises access to virtually unlimited cloud storage.

AWS Storage Gateway `uses SSL/TLS` (Secure Socket Layers/Transport Layer Security) `to encrypt data` that is transferred `between your gateway appliance and AWS storage`. By default, Storage Gateway uses Amazon S3-Managed Encryption Keys (SSE-S3) to server-side encrypt all data it stores in Amazon S3. You have an option to use the Storage Gateway API to configure your gateway to encrypt data stored in the cloud using server-side encryption with AWS Key Management Service (SSE-KMS) customer master keys (CMKs).

File, Volume and Tape Gateway data is stored in Amazon S3 buckets by AWS Storage Gateway. Tape Gateway supports backing data to Amazon S3 Glacier apart from the standard storage.

Encrypting a file share: For a file share, you can configure your gateway to encrypt your objects with AWS KMS–managed keys by using SSE-KMS.

Encrypting a volume: For cached and stored volumes, you can configure your gateway to encrypt volume data stored in the cloud with AWS KMS–managed keys by using the Storage Gateway API.

Encrypting a tape: For a virtual tape, you can configure your gateway to encrypt tape data stored in the cloud with AWS KMS–managed keys by using the Storage Gateway API.

### Tape Gateway
Tape Gateway enables you to replace using physical tapes on-premises with virtual tapes in AWS without changing existing backup workflows. Tape Gateway supports all leading backup applications and caches virtual tapes on-premises for low-latency data access. Tape Gateway encrypts data between the gateway and AWS for secure data transfer and compresses data and transitions virtual tapes between Amazon S3 and Amazon S3 Glacier, or Amazon S3 Glacier Deep Archive, to minimize storage costs.

### File Gateway
File Gateway provides a seamless way to connect to the cloud in order to store application data files and backup images as durable objects in Amazon S3 cloud storage. File Gateway offers `SMB or NFS-based` access to data in Amazon S3 with local caching.

### Volume Gateway
You can configure the AWS Storage Gateway service as a Volume Gateway to present `cloud-based iSCSI block` storage volumes to your `on-premises` applications. The Volume Gateway provides either a local cache or full volumes on-premises while also storing full copies of your volumes in the AWS cloud. Volume Gateway also provides Amazon EBS Snapshots of your data for backup, disaster recovery, and migration. It's easy to get started with the Volume Gateway: Deploy it as a virtual machine or hardware appliance, give it local disk resources, connect it to your applications, and start using your hybrid cloud storage for block data.

Reference: [AWS Storage Gateway](https://aws.amazon.com/storagegateway/)

## AWS Directory Services
service that automatically creates an AWS security group in your VPC with network rules for traffic in and out of AWS managed domain controllers. The default inbound rules allow traffic from any source (0.0.0.0/0) to ports required by Active Directory. These rules do not introduce security vulnerabilities, as traffic to the domain controllers is limited to traffic from your VPC, other peered VPCs, or networks connected using AWS Direct Connect, AWS Transit Gateway or Virtual Private Network.

`By default`, AWS Directory Services creates security groups that `allow unrestricted access`, which can be `flagged as a security concern. To address this issue, you need to review the security group rules and make necessary adjustments to restrict access based on your specific requirements and security best practices.

Using `AWS Trusted Advisor` can provide additional insights into security best practices and potential misconfigurations, but it may not specifically highlight the security group issue related to AWS Directory Services.

## Enhanced networking
Consider using enhanced networking for the following scenarios:

1. If your packets-per-second rate reaches its ceiling, consider moving to enhanced networking. If your rate reaches its ceiling, you've likely reached the upper thresholds of the virtual network interface driver.
1. If your throughput is near or exceeding 20K packets per second (PPS) on the VIF driver, it's a best practice to use enhanced networking.

All current generation instance types support enhanced networking, except for T2 instances.

## Cost Allocation Tags
A tag is a label that you or AWS assigns to an AWS resource. Each tag consists of a key and a value. For each resource, each tag key must be unique, and each tag key can have only one value. You can use tags to organize your resources, and cost allocation tags to track your AWS costs on a detailed level. After you activate cost allocation tags, AWS uses the cost allocation tags to organize your resource costs on your cost allocation report, to make it easier for you to categorize and track your AWS costs.

## `*Q` [AWS Resource Groups Tag Editor](https://docs.aws.amazon.com/ARG/latest/userguide/tag-editor.html)
With Resource Groups, you can create, maintain, and view a collection of resources that share common tags. Tag Editor manages tags across services and AWS Regions. Tag Editor can perform a global search and can edit a large number of tags at one time.

## Aurora DB

### Connect to Amazon Aurora DB cluster from outside a VPC
To connect to an Amazon Aurora DB cluster directly from outside the VPC, the instances in the cluster must meet the following requirements:

1. The DB instance must have a public IP address.
1. The DB instance must be running in a publicly accessible subnet.

For Amazon Aurora DB instances, you can't choose a specific subnet. Instead, choose a DB subnet group when you create the instance. Create a DB subnet group with subnets of similar network configuration. For example, a DB subnet group for Public subnets.

### Metrics to generate reports on the Aurora DB Cluster and its replicas
1. `AuroraReplicaLagMaximum` - This metric captures the `maximum amount of lag between the primary instance and each Aurora DB instance in the DB cluster`.
1. `AuroraBinlogReplicaLag` - This metric captures the `amount of time a replica DB cluster running` on Aurora MySQL-Compatible Edition lags behind the source DB cluster.
This metric reports the value of the Seconds_Behind_Master field of the MySQL SHOW SLAVE STATUS command. This metric is useful for monitoring replica lag between Aurora DB clusters that are replicating across different AWS Regions.
1. `AuroraReplicaLag` - This metric captures the `amount of lag` an Aurora replica experiences `when replicating updates from the primary instance`.
1. `InsertLatency` - This metric captures `the average duration of insert operations`.

## Aurora Reader Endpoint
To perform queries, you can connect to the reader endpoint, with Aurora automatically performing load-balancing among all the Aurora Replicas.

A reader endpoint for an Aurora DB cluster provides load-balancing support for read-only connections to the DB cluster. Use the reader endpoint for read operations, such as queries. By processing those statements on the read-only Aurora Replicas, this endpoint reduces the overhead on the primary instance. It also helps the cluster to scale the capacity to handle simultaneous SELECT queries, proportional to the number of Aurora Replicas in the cluster. Each Aurora DB cluster has one reader endpoint.

Reference:[Amazon Aurora connection management](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.Endpoints.html)

## RDS

### [RDS storage autoscaling](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.StorageTypes.html#USER_PIOPS.Autoscaling)
With RDS storage autoscaling, you can set the desired maximum storage limit. Autoscaling will manage the storage size. RDS storage autoscaling monitors actual storage consumption and then scales capacity automatically when actual utilization approaches the provisioned storage capacity.

## AWS Systems Manager Inventory
AWS Systems Manager Inventory provides visibility into your `Amazon EC2` and `on-premises` computing environment. You can use Inventory to `collect metadata` from your `managed instances`. You can store this metadata in a central Amazon Simple Storage Service (Amazon S3) bucket, and then use built-in tools to query the data and quickly determine which instances are running the software and configurations required by your software policy, and which instances need to be updated. You can configure Inventory on all of your managed instances by using a one-click procedure. You can also configure and view inventory data from multiple AWS Regions and AWS accounts.

If the pre-configured metadata types collected by Systems Manager Inventory don't meet your needs, then you can create custom inventory. `Custom inventory` is simply a JSON file with information that you provide and add to the managed instance in a specific directory. When Systems Manager Inventory collects data, it captures this custom inventory data.

Systems Manager Inventory collects only metadata from your managed instances. Inventory doesn't access proprietary information or data.

## OpsWorks
AWS OpsWorks is a `configuration management service` that provides managed instances of `Chef` and `Puppet`.

## AWS Personal Health Dashboard
AWS Personal Health Dashboard provides `alerts and remediation guidance when AWS is experiencing events that may impact you`. While the Service Health Dashboard displays the general status of AWS services, Personal Health Dashboard gives you a personalized view into the performance and availability of the AWS services underlying your AWS resources.

What’s more, Personal Health Dashboard proactively notifies you when AWS experiences any events that may affect you, helping provide quick visibility and guidance to help you minimize the impact of events in progress, and plan for any scheduled changes, such as AWS hardware maintenance.AWS Inspector

The `AWS Health API provides` programmatic `access` to the `AWS Health information` that appears in the AWS Personal Health Dashboard. You can use the API operations to get information about events that might affect your AWS services and resources.

## Cost Allocation Tags
A tag is a label that you or AWS assigns to an AWS resource. Each tag consists of a key and a value. For each resource, each tag key must be unique, and each tag key can have only one value. You can use tags to organize your resources, and cost allocation tags to track your AWS costs on a detailed level. After you activate cost allocation tags, AWS uses the cost allocation tags to organize your resource costs on your cost allocation report, to make it easier for you to categorize and track your AWS costs.

## [Protecting data using encryption](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingEncryption.html)

### SSE-S3 - Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)
Using SSE-S3 each object is encrypted with a unique key employing strong multi-factor encryption. As an additional safeguard, it encrypts the key itself with a master key that it regularly rotates. Amazon S3 server-side encryption uses one of the strongest block ciphers available, 256-bit Advanced Encryption Standard (AES-256), to encrypt your data.

### SSE-KMS
Similar to SSE-S3 and also `provides` you with an `audit trail` of when your key was used and by whom. Additionally, you have the `option` to `create` and `manage encryption keys yourself`.

### SSE-C
`You manage the encryption keys` and `Amazon S3 manages the encryption` as it writes to disks and decryption when you access your objects.

### Client-Side Encryption
You can encrypt data client-side and upload the encrypted data to Amazon S3. In this case, you manage the encryption process, the encryption keys, and related tools.

## AWS Elastic Beanstalk
With deployment policies such as 'All at once', AWS Elastic Beanstalk performs an in-place update when you update your application versions and your application can become unavailable to users for a short period of time. You can avoid this downtime by performing a blue/green deployment, where you deploy the new version to a separate environment, and then swap CNAMEs (via Route 53) of the two environments to redirect traffic to the new version instantly. In case of any deployment issues, the rollback process is very quick via swapping the URLs for the two environments.

Reference: [Deploying applications to Elastic Beanstalk environments](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.deploy-existing-version.html)

## Dedicated Hosts and Dedicated Instances

## [Dedicated Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-instance.html)
Are Amazon EC2 instances that run in a virtual private cloud (VPC) on `hardware` that's `dedicated` to a `single customer`. Dedicated Instances that belong to different AWS accounts are physically isolated at a hardware level, even if those accounts are linked to a single-payer account. `Note` that Dedicated Instances may share hardware with other instances from the same AWS account that are not Dedicated Instances.

Dedicated Hosts allow you to use your existing per-socket, per-core, or per-VM software licenses, including Windows Server, Microsoft SQL Server, SUSE, and Linux Enterprise Server

## [Dedicated Host](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-hosts-overview.html)
Is a `physical server` with EC2 instance capacity fully dedicated to your use

- Dedicated Hosts `allow` you to `use` your `existing software licenses` on EC2 instances. With a Dedicated Host, you have ``visibility and control`` over how ``instances`` are placed on the server.
- Dedicated Hosts allow you to use your existing `per-socket`, `per-core`, or `per-VM software licenses`, including `Windows Server`, `Microsoft SQL Server`, `SUSE`, and `Linux Enterprise Server`.

Reference: [Dedicated Hosts](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-hosts-overview.html#dedicated-hosts-dedicated-instances)

## AWS Organizations
If you have created an organization in AWS Organizations, you can also create a trail that will log all events for all AWS accounts in that organization. This is referred to as an organization trail.

## [AWS CloudHSM (Hardware Security Module)](https://docs.aws.amazon.com/cloudhsm/latest/userguide/clusters.html)
AWS CloudHSM provides dedicated `hardware security` modules to store and `manage cryptographic KEYS securely`. It offers `FIPS 140-2 Level 3` validated HSMs, which are ideal for meeting compliance requirements. With CloudHSM, you have full control over the key lifecycle and can perform key operations within the HSM, ensuring strong security and compliance for your keys.

## AWS Service Catalog
AWS Service Catalog allows organizations to create and manage catalogs of IT services that are approved for use on AWS. These IT services can include everything from virtual machine images, servers, software, and databases to complete multi-tier application architectures. AWS Service Catalog allows you to centrally manage deployed IT services and your applications, resources, and metadata. This helps you achieve consistent governance and meet your compliance requirements while enabling users to quickly deploy only the approved IT services they need.

#### [Sharing and Importing Portfolios](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/catalogs_portfolios_sharing.html)
To make your Service Catalog products available to users who are not in your AWS accounts, such as users who belong to other organizations or to other AWS accounts in your organization, you share your portfolios with them. You can share in several ways, including `account-to-account` sharing, `organizational` sharing, and `deploying catalogs using stack sets`.

Before you share your products and portfolios to other accounts, you must decide whether you want to share a reference of the catalog or to deploy a copy of the catalog into each recipient account. Note that if you deploy a copy, you must redeploy if there are updates you want to propagate to the recipient accounts.

You can use stack sets to deploy your catalog to many accounts at the same time. If you want to share a reference (an imported version of your portfolio that stays in sync with the original), you can use account-to-account sharing or you can share using AWS Organizations.

## Amazon EFS

### Enforce creation that is encrypted at rest
* Use the `elasticfilesystem:Encrypted` IAM condition key in AWS IAM identity-based policies to mandate users for creating only encrypted-at-rest Amazon EFS file systems

You can create an AWS Identity and Access Management (IAM) identity-based policy to control whether users can create Amazon EFS file systems that are encrypted at rest. The Boolean condition key elasticfilesystem:Encrypted specifies the type of file system, encrypted or unencrypted, that the policy applies to. You use the condition key with the elasticfilesystem:CreateFileSystem action and the policy effect, allow or deny, to create a policy for creating encrypted or unencrypted file systems.

* Define `Service Control Policies (SCPs)` inside `AWS Organizations` to enforce EFS encryption for all AWS accounts in your organization.

Service control policies (SCPs) are a type of organization policy that you can use to manage permissions in your organization. SCPs offer central control over the maximum available permissions for all accounts in your organization.

An SCP restricts permissions for IAM users and roles in member accounts, including the member account's root user. If a user or role has an IAM permission policy that grants access to an action that is either not allowed or explicitly denied by the applicable SCPs, the user or role can't perform that action. You can also define service control policies (SCPs) inside AWS Organizations to enforce EFS encryption for all AWS accounts in your organization.

### EC2 instances are unable to mount the file system.
The `security groups` that you associate with a mount target must allow inbound access for the `TCP protocol` on the `NFS port` `from` the `security group` used by the instances.
To connect your Amazon EFS file system to your Amazon EC2 instance, you `must create two security groups`: `one` for your Amazon `EC2 instance` and `another` for your Amazon `EFS mount target`.

Reference: [Creating security groups](https://docs.aws.amazon.com/efs/latest/ug/accessing-fs-create-security-groups.html)

## Amazon Inspector
It is an automated security assessment `service` that `helps improve the security and compliance` of `applications deployed on AWS`.
Amazon Inspector checks for `unintended network accessibility` of your Amazon EC2 instances and vulnerabilities on those EC2 instances.

## AWS Control Tower
Offers the easiest way to `set up` and `govern` a `secure, multi-account AWS environment`. It establishes a landing zone that is based on the best-practices blueprints and enables governance using guardrails you can choose from a pre-packaged list. The landing zone is a well-architected, multi-account baseline that follows AWS best practices. Guardrails implement governance rules for security, compliance, and operations.

## AWS WAF (Web Application Firewall)
AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to an Amazon `CloudFront` distribution, an Amazon `API Gateway` REST API, an `Application Load Balancer`, or an `AWS AppSync GraphQL API`.

### `*Q` [Change AWS Firewall Manager administration account](https://docs.aws.amazon.com/waf/latest/developerguide/fms-change-administrator.html)
You can designate `only one account in` an `organization as a Firewall Manager administrator account`. To create a new Firewall Manager administrator account, you must revoke the original administrator account first.

## AWS X-Ray
1. `S3` - AWS X-Ray integrates with Amazon S3 to trace upstream requests to update your application's S3 buckets.
1. `Lambda functions` - Lambda runs the X-Ray daemon and records a segment with details about the function invocation and execution.
1. `API Gateway APIs` - You can use X-Ray to trace and analyze user requests as they travel through your Amazon API Gateway APIs to the underlying services.

## DNS Resolution
DNS Resolution is used to enable resolution of public DNS hostnames to private IP addresses when queried from the [peered VPC](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html).

## ASG

### Classic Load Balancer

#### Metrics
`SpilloverCount` represents the total `number of requests` that were `rejected` `because` the surge `queue` is `full`.

To solve this use-case, you need to configure the Auto Scaling groups to scale your instances based on the `SurgeQueueLength` metric.

## [Traffic Mirroring](https://docs.aws.amazon.com/vpc/latest/mirroring/what-is-traffic-mirroring.html)
Traffic Mirroring provides the ability to create a copy of a packet flow to examine the contents of a packet. This feature is useful for `threat monitoring`, `content inspection`, and `troubleshooting`.

A packet is truncated to the `MTU` value when both of the following are true:

- The traffic mirror target is a standalone instance.
- The traffic packet size from the mirror source is greater than the MTU size for the traffic mirror target.

## `*Q` [SAML federation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_saml.html)
- `SAML federation between AWS and` the corporate `Active Directory and mapping Active Directory groups to IAM groups` is the recommended way to make access more secure and streamlined.