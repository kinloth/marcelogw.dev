---
title: "Elastic Compute Cloud"
date: 2022-04-07
description: AWS EC2
hero: "images/hero.jpg"
menu:
  sidebar:
    name: EC2
    identifier: aws-ec2
    parent: aws
    weight: 10
tags: ["AWS", "Storage", "Cloud", "EC2"]
categories: ["AWS", "EC2"]
---

### About

Cloud Computing Services

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides resizable compute capacity in the cloud.
It is designed to make web-scale computing easier for developers. It takes minutes to launch new instances.
Anything and everything on AWS uses EC2 instance undernath.

It supports machines from nano (1vCPU) and 0.5GB mem to 112xlarge with 448vCPU and 12288Gb mem.

EC2 is hosted on the concept of server virtualization, where the full computing power of server hardware can be divided into various instances and offered to the end-user as a computing instance over the internet.

{{< alert type="success" >}}
Free Tier: 750 hours per month for 12 months in specific machines.
{{< /alert >}}

### Instances

A virtual server used for running applications on Amazon’s EC2 is an instance. An instance can be understood as a small part of a large computer, having its own hard drive, network connection, OS, etc. You can have multiple small computers on a single physical machine, and all these small machines are called Instances.

### Instance types

As of January 2022, the following instance types were offered:

#### General Purpose
General purpose instances provide a balance of compute, memory and networking resources, and can be used for a variety of diverse workloads. These instances are ideal for applications that use these resources in equal proportions such as web servers and code repositories.

{{< alert type="success" >}}
Machines: Mac, T4g, T3, T3a, T2, M6g, M6i, M6a, M5, M5a, M5n, M5zn, M4, A1
{{< /alert >}}

{{< vs 2 >}}

#### Compute Optimized
Compute Optimized instances are ideal for compute bound applications that benefit from high performance processors. Instances belonging to this family are well suited for batch processing workloads, media transcoding, high performance web servers, high performance computing (HPC), scientific modeling, dedicated gaming servers and ad server engines, machine learning inference and other compute intensive applications.

{{< alert type="success" >}}
Machines: C7g, C6g, C6gn, C6i, C6a, Hpc6a, C5, C5a, C5n, C4
{{< /alert >}}

{{< vs 2 >}}

#### Memory Optimized
Memory optimized instances are designed to deliver fast performance for workloads that process large data sets in memory.

{{< alert type="success" >}}
Machines: R6g, R6i, R5, R5a, R5b, R5n, R4, X2gd, X2idn, X2iedn, X1e, X1, High Memory, z1d
{{< /alert >}}

{{< vs 2 >}}

#### Accelerated Computing
Accelerated computing instances use hardware accelerators, or co-processors, to perform functions, such as floating point number calculations, graphics processing, or data pattern matching, more efficiently than is possible in software running on CPUs.

{{< alert type="success" >}}
Machines: P4, P3, P2, DL1, Trn1, Inf1, G5, G5g, G4dn, G3, F1, VT1
{{< /alert >}}

{{< vs 2 >}}

#### Storage Optimized
Storage optimized instances are designed for workloads that require high, sequential read and write access to very large data sets on local storage. They are optimized to deliver tens of thousands of low-latency, random I/O operations per second (IOPS) to applications.

{{< alert type="success" >}}
Machines: Im4gn, Is4gen, I4i, I3, I3gen, D2, D3, D3en, H1
{{< /alert >}}

{{< vs 4 >}}

### Instances pay types

{{< vs 1 >}}
#### On-Demand
There are no long term commitments in case of On-Demand Instances. They charge you for the compute capacity used per hour. Companies can increase or decrease the capacity depending on the demand of their application and will only pay for the specified hourly rate of the instance they choose. The benefit of using On-Demand instance is that it saves you from the cost of managing, planning, and purchasing hardware and converts your large fixed costs into smaller variable costs. It also eliminates the need for “safety net” capacity to handle sudden traffic spikes.

{{< vs 1 >}}
#### Reserved
In Reserved Instances, there is a flexibility to change operating system types and tenancies. RI has an optional capacity reservation for EC2 instances. AWS Billing applies discounted rates of RIs when the attributes of EC2 instance’s usage matches with that of an active RI.

EC2 reserves capacity matching the attributes of RI, if an Availability Zone (AZ) is specified. The running instances automatically utilize the capacity reservation of RI which matches its attributes.

{{< vs 1 >}}
#### Spot
Amazon EC2 Spot Instances let you take advantage of unused EC2 capacity in the Amazon Web Services cloud.
You can use Spot Instances for various stateless, fault-tolerant, or flexible applications such as big data, containerized workloads, CI/CD, web servers, high-performance computing (HPC), and other test & development workloads.

{{< alert type="success" >}}
Spot Instances are available at up to a 90% discount compared to On-Demand prices.
{{< /alert >}}

{{< vs 4 >}}
### Benefits

##### Reliability

Amazon EC2 offers 99.9% availability for each Amazon EC2 region. The services are highly reliable where replacement of instances can be done easily and rapidly.

##### Security

Amazon works with Amazon VPC to provide robust networking and security for the compute resources. The compute instances are located in a VPC (Virtual Private Cloud) in a specific IP range. This specific function helps the user in deciding which instances are exposed to the internet and which remains private.

##### Flexibility

EC2 provides you with choices of multiple instance types, software packages, instance storages, and operating systems. EC2 lets us configure memory, CPU and boot partition size which is optimal for the operating system and application.

##### Cost Saving

EC2 is inexpensive as it allows the user to select plans as per the requirement. This will help the user to save cost and utilize the resources fully. EC2 passes the benefits of Amazon’s scale as the user has to pay a very low amount compared to the services they provide.

##### Complete Computing Solution

EC2 works fine with Amazon RDS, S3, Dynamo DB and Amazon SQS. This provides complete computing, processing and storage solution.

##### Elastic Web-Scale Computing
Enterprises can easily increase or decrease capacity within minutes. They can commission thousands of server instances simultaneously. Additionally, all the server instances are handled by the web service APIs which can scale the servers up and down depending on the requirements.

##### Completely controlled

One has complete control over the instances. Also, One can have root access to each instance and they can interact with them as any other machine. The user can stop instance while retaining the data on the boot partition and restart the same using web service APIs.

{{< vs 4 >}}
### Best practices

AWS tips to best practices in EC2. For more information, check the link in references:

Security
- Manage access to AWS resources and APIs using identity federation, IAM users, and IAM roles. Establish credential management policies and procedures for creating, distributing, rotating, and revoking AWS access credentials.
- Usage of least permissive rules for security groups.
- Regularly patch, update, and secure the operating system and applications on your instance.
- Use Amazon Inspector to automatically discover and scan Amazon EC2 instances for software vulnerabilities and unintended network exposure

{{< vs 1 >}}

Storage
- Understand the implications of the root device type for data persistence, backup, and recovery.
- Separate Encrypted EBS volumes for the operating system data.
- Use the instance store available for your instance to store temporary data. Remember that the data stored in instance store is deleted when you stop, hibernate, or terminate your instance. If you use instance store for database storage, ensure that you have a cluster with a replication factor that ensures fault tolerance.

{{< vs 1 >}}

Resource management
- Use instance metadata and custom resource tags to track and identify your AWS resources.
- View your current limits for Amazon EC2. Plan to request any limit increases in advance of the time that you'll need them.

{{< vs 1 >}}

Backup and recovery
- Regularly back up EBS volumes using snapshots, and create an Amazon Machine Image (AMI) from instances to save the configuration as a template for launching future instances.
- Deploy critical components of application across multiple Availability Zones, and replicate the data appropriately.
- Design your applications to handle dynamic IP addressing when your instance restarts.
- Ensure that you are prepared to handle failover. For a basic solution, you can manually attach a network interface or Elastic IP address to a replacement instance. For more information, see Elastic network interfaces. For an automated solution, you can use Amazon EC2 Auto Scaling.
- Regularly test the process of recovering your instances and EBS volumes if they fail.

{{< vs 1 >}}

Networking
- Set the time-to-live (TTL) value for your applications to 255, for IPv4 and IPv6. If you use a smaller value, there is a risk that the TTL will expire while application traffic is in transit, causing reachability issues for your instances.


{{< vs 4 >}}
### References
- Main AWS EC2 page: https://aws.amazon.com/ec2/
- Wikipedia: https://pt.wikipedia.org/wiki/Amazon_EC2
- Best Practices: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-best-practices.html
- Instance Types: https://aws.amazon.com/ec2/instance-types/
- Instance Types CN: https://www.amazonaws.cn/en/ec2/instance-types/
- Security: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Instances.html
- FAQs: https://aws.amazon.com/ec2/faqs/