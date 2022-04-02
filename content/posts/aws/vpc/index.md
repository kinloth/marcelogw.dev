---
title: "Virtual Private Cloud"
date: 2022-04-02
description: AWS VPC
hero: "images/hero.jpg"
menu:
  sidebar:
    name: VPC
    identifier: aws-vpc
    parent: aws
    weight: 10
tags: ["AWS", "Storage", "Cloud", "VPC"]
categories: ["AWS", "VPC"]
---

### About
It manages how your applications are distributed inside AWS servers, and more importantly, how will be the network access of these applications for in and out network connections.

The AWS Cloud is distributed in regions and availability zones (AZ) around the world. With VPC we can get access to this infrastructure, a logically isolated section, to control the virtual networking environment, including resource placement, connectivity, and security.


{{< img src="images/intro.png" height="70%" width="70%" align="center" title="intro" >}}

In the example above, network traffic is being shared between two VPCs in single Region.

{{< vs 3 >}}

#### VPC Components

The VPC is made from the following services:
- Public Subnets
- Private Subnets
- VPC Peering
- Routing Tables
- Internet Gateway (IGW)
- Security Groups (SG)
- Network Access Control Lists (NACLs)
- Nat Gateway
- VPC Endpoints

A simple schema with core components:
{{< img src="images/components.png" height="90%" width="90%" align="center" title="components" >}}

{{< vs 4 >}}

#### Default VPC
Each Amazon account comes with a default VPC that is pre-configured for you to start using immediately.


This is the diagram of a default VPC:

{{< img src="images/default.png" height="80%" width="80%" align="center" title="default" >}}

{{< alert type="info" >}}
A VPC can span multiple availability zones in a region.
{{< /alert >}}

{{< vs 4 >}}

### VPC Peering

Allows you to connect one VPC with another over a direct network route using private IP addresses.

Instances on peered VPCs behave just like they are on the same network

Connect VPCs across the same or different AWS accounts and regions:

{{< img src="images/peering.png" height="100%" width="100%" align="center" title="peering" >}}

{{< alert type="warning" >}}
No Transitive Peering (peering must take place directly between VPCs) and no Overlapping CIDR Blocks.
{{< /alert >}}

{{< vs 4 >}}


### Route tables
It is used to determine where network traffic is directed.

Each subnet in your VPC must be associated with a RouteTable.


{{< img src="images/route_table.png" height="80%" width="80%" align="center" title="route table" >}}

{{< alert type="secondary" >}}
A subnet can only be associated with one route table at a time, but you can associate multiple subnets with the same route table.
{{< /alert >}}

{{< vs 4 >}}


### Internet Gateway
The Internet Gateway allows your VPC access to the internet.

IGW does two things:
1. provide a target in your VPC route tables for internet
2. routable traffic perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.


{{< img src="images/internet_gateway.png" height="80%" width="80%" align="center" title="internet gateway" >}}

{{< alert type="secondary" >}}
To route out to the internet you need to add in your route tables the internet gateway address and set the Destination to be 0.0.0.0/0.
{{< /alert >}}

{{< vs 4 >}}


### Security Groups
Acts as a virtual firewall at the instance level.

Security Groups are associated with EC2 instances.

Each Security Group contains a set of rules that filter traffic coming into (inbound) and out of (outbound) EC2 instances.

There are no ‘Deny’ rules: All traffic is blocked by default unless a rule specifically allows it.

Multiple Instances across multiple subnets can belong to a Security Group.

{{< img src="images/security_groups.png" height="85%" width="85%" align="center" title="security_groups" >}}


##### Uses Cases

You can specify the source to be an IP range or A specific ip (/32 is a specific IP Address):
{{< img src="images/security_groups_case1.png" height="70%" width="70%" align="center" title="case 1" >}}
{{< vs 1 >}}

You can specify the source to be another security group:
{{< img src="images/security_groups_case2.png" height="70%" width="70%" align="center" title="case 2" >}}
{{< vs 1 >}}

An instance can belong to multiple Security Groups, and rules are permissive (instead of restrictive). Meaning if you have one security group which has no Allow and you add an allow to another than it will Allow:
{{< img src="images/security_groups_case3.png" height="70%" width="70%" align="center" title="case 3" >}}
{{< vs 4 >}}


### NACLs
Network Access Control List (NACLs) acts as a virtual firewall at the subnet level:
{{< img src="images/nacl.png" height="80%" width="80%" align="center" title="nacl" >}}

VPCs automatically get a default NACL. The Subnets are associated with NACLs. Subnets can only belong to a single NACL.

Each NACL contains a set of rules that can allow or deny traffic into (inbound) and out of (outbound) subnets. You can allow or deny traffic:

{{< img src="images/nacl_traffic.png" height="55%" width="55%" align="center" title="nacl traffic" >}}

Rule # determines the order of evaluation. From lowest to highest.

The highest rule # can be 32766 and it's recommended to work in 10 or 100 increments.

{{< alert type="info" >}}
You could block a single IP address (You can’t do this with Security Groups)
{{< /alert >}}

<!--
NACLs Cheatsheet
Network Access Control List is commonly known as NACL
VPCs are automatically given a default NACL which allows all outbound and inbound traffic.
Each subnet within a VPC must be associated with an NACL
Subnets can only be associated with 1 NACL at a time. Associating a subnet with a new NACL will remove the previous association.
If an NACL is not explicitly associated with a subnet, the subnet will automatically be associated with the default NACL.
NACL has inbound and outbound rules (just like Security Groups).
The rule can either allow or deny traffic. (unlike Security Groups which can only allow)
NACLs are STATELESS (any allowed inbound traffic is also allowed outbound)
CORRECTION: NACLs are STATELESS (incoming rule will not be applied to the outgoing)
When you create an NACL it will deny all traffic by default
NACLs contain a numbered list of rules that get evaluated in order from lowest to highest.
If you needed to block a single IP address you could via NACLs (Security Groups cannot deny) -->

{{< vs 4 >}}

### Network Address Translation (NAT)

Network Address Translation (NAT) is the method of re-mapping one IP address space into another.

If you have a private network and you need to help gain outbound access to the internet, you would need to use a NAT gateway to re-map the Private IPs

If you have two networks that have conflicting network addresses, you can use a NAT to make the addresses more agreeable

{{< img src="images/nat_gateway.png" height="75%" width="75%" align="center" title="nat gateway" >}}

{{< vs 4 >}}


### VPC endpoints
Think of a secret tunnel where you don’t have to leave the AWS network.

VPC Endpoints allow you to privately connect your VPC to other AWS services, and VPC endpoint services.

{{< img src="images/vpc_endpoints.png" height="75%" width="75%" align="center" title="vpc endpoints" >}}

There are two types of VPC Endpoints:
1. Interface Endpoints
2. Gateway Endpoints

Eliminates the need for an Internet Gateway, NAT device, VPN connection, or AWS Direct Connect connections.

Instances in the VPC do not require a public IP address to communicate with service resources.

Traffic between your VPC and other services does not leave the AWS network.

Horizontally scaled, redundant, and highly available VPC component.

Allows secure communication between instances and services - without adding availability risks or bandwidth constraints on your traffic.

{{< vs 2 >}}

#### Interface endpoint
Interface Endpoints are Elastic Network Interfaces (ENI) with a private IP address.

They serve as an entry point for traffic going to a supported service.

{{< img src="images/interface_endpoint.png" height="75%" width="75%" align="center" title="interface endpoint" >}}

Access services hosted on AWS easily and securely by keeping your network traffic within the AWS network.

Interface Endpoints support the following AWS Services:
- API Gateway
- CloudFormation
- CloudWatch
- Kinesis
- SageMaker
- Codebuild
- AWS Config
- EC2 API
- ELB API
- AWS KMS
- Secrets Manager
- Security Token Service
- Service Catalog
- SNS
- SQS
- Systems Manager
- Marketplace Partner Services
- Endpoint Services in other AWS accounts

{{< vs 2 >}}

#### Gateway endpoint

A Gateway Endpoint is a gateway that is a target for a specific route in your route table, used for traffic destined for a supported AWS service.

{{< img src="images/gateway_endpoint.png" height="75%" width="75%" align="center" title="gateway endpoint" >}}

To create a Gateway Endpoint, you must specify the VPC in which you want to create the endpoint, and the service to which you want to establish the connection.

AWS Gateway Endpoint currently only supports two services:
- Amazon S3
- DynamoDB

{{< alert type="info" >}}
VPC Gateway Endpoints are Free!
{{< /alert >}}

{{< vs 4 >}}

### Extra

#### VPC Flow Logs
Allow you to capture IP traffic information in and out of Network Interfaces within your VPC.

{{< img src="images/flow_logs.png" height="75%" width="75%" align="center" title="flow logs" >}}

You can create flow logs for network interfaces that are created by other AWS services, such as:

- Elastic Load Balancing
- Amazon RDS
- Amazon ElastiCache
- Amazon Redshift
- Amazon WorkSpaces
- NAT gateways
- Transit gateways


All log data is stored using Amazon CloudWatch Logs or S3 bucket.

After a Flow Log is created it can be viewed in detail within CloudWatch Logs.

{{< vs 2 >}}

#### Direct Connect

AWS solution for establishing dedicated network connections from on-premises locations to AWS.

{{< img src="images/direct_connect.png" height="95%" width="95%" align="center" title="direct connect" >}}

Helps reduce network costs and increase bandwidth throughput. (great for high traffic networks).

Provides a more consistent network experience than a typical internet-based connection. (reliable and secure).

{{< alert type="primary" >}}
Very fast network Lower Bandwidth 50M-500M or Higher Bandwidth 1GB or 10GB.
{{< /alert >}}

{{< vs 3 >}}

### References
- Main AWS page: https://aws.amazon.com/vpc/
- Pricing: https://aws.amazon.com/vpc/pricing/
- Features: https://aws.amazon.com/vpc/features/
- FAQs: https://aws.amazon.com/vpc/faqs/
- AWS Solutions Architect tutorial video: https://www.youtube.com/watch?v=Ia-UEYYR44s/
- AWS VPC tutorial: https://www.simplilearn.com/tutorials/aws-tutorial/aws-vpc/
- Direct Connect: https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html
- Flow Logs: https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html
- Interface Endpoint (Private Link): https://docs.aws.amazon.com/vpc/latest/privatelink/vpce-interface.html
- Gateway Endpoints: https://docs.aws.amazon.com/vpc/latest/privatelink/vpce-gateway.html