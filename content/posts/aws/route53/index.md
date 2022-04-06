---
title: "Route 53"
date: 2022-04-02
description: AWS Route 53
hero: "images/hero.jpg"
menu:
  sidebar:
    name: Route 53
    identifier: aws-route53
    parent: aws
    weight: 10
tags: ["AWS", "Storage", "Cloud", "Route 53"]
categories: ["AWS", "Route 53"]
---

### About

Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service.
Much like Godaddy and NameCheap, but with more synergies with others AWS services.

It is designed to give developers and businesses an extremely reliable and cost effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other.


It has a bunch of features, some them are:
- Register and manage domains
- Create various records sets on a domain
- Implement complex traffic flows eg. Blue/green deploy, fail-overs
- Continuously monitor records via health checks
- Resolve VPC’s outside of AWS

{{< vs 4 >}}
### Use Cases

For route in Route53, we could point the Incoming internet traffic to:
- A web-app backed by ALB (Application Load Balancer).
- An instance we use to tweak our AMI (Amazon Machine Images).
- API gateway which powers our API (Application Programming Interface).
- CloudFront which serves our S3 static hosted website.
- An Elastic IP (EIP) which is a static IP that hosts our company server.

{{< vs 4 >}}
### Record set

It's possible to create a record sets that allow us to point a naked domain (example.com) and subdomains (www) via Domain records.
For example, we can send a www subdomain using an A record to point to a specific IP address:

`www.example.com -> 120.119.2.53`

AWS has its own special Alias Record which extends DNS functionality. It will route traffic to specific AWS resources, like API Gateway.

{{< alert type="success" >}}
Alias records are smart where they can detect the change of an IP address and continuously keep that endpoint pointed to the correct resource.
{{< /alert >}}


{{< vs 4 >}}
### Route53 - Routing Policies

There are 7 different types of Routing Policies available inside Route53

- Simple Routing: Default routing policy, multiple addresses result in a random selection.
- Weighted Routing: Route traffic based on weighted values to split traffic.
- Latency-Based Routing: Route traffic to region resource with the lowest latency.
- Failover Routing: Route traffic if primary endpoint is unhealthy to the secondary endpoint.
- Geolocation Routing: Route traffic based on the location of your users.
- Geo-proximity Routing: Route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.
- Multi-value Answer Routing: Responds to DNS queries with up to eight healthy records selected at random.

{{< vs 4 >}}
### Health check

Amazon Route 53 health checks monitor the health and performance of your web applications, web servers, and other resources.

Each health check that you create can monitor one of the following:

- The health of a specified resource, such as a web server.
- The status of other health checks.
- The status of an Amazon CloudWatch alarm.
- Additionally, with Amazon Route 53 Application Recovery Controller, you can set up routing control health checks with DNS failover records to manage traffic failover for your application

Checks health every 30s by default. Can be reduced down to every 10s.

A health check can initial a failover if the status is returned unhealthy.

{{< alert type="info" >}}
A health check can monitor other health checks to create a chain of reactions.
{{< /alert >}}

{{< vs 4 >}}
### References
- Main AWS page: https://aws.amazon.com/route53/features/
- FAQs: https://aws.amazon.com/route53/faqs/
- Guide: https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html
- DNS Complex configs - https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover-complex-configs.html
- Concepts: https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/route-53-concepts.html
- Failover: https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover.html