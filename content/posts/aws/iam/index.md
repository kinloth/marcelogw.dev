---
title: "Identity Access Management"
date: 2022-04-02
description: AWS IAM
hero: "images/hero.jpg"
menu:
  sidebar:
    name: IAM
    identifier: aws-iam
    parent: aws
    weight: 10
tags: ["AWS", "Storage", "Cloud", "IAM"]
categories: ["AWS", "IAM"]
---

### About
AWS Identity and Access Management (IAM) provides fine-grained access control across all of AWS.

With IAM, you can specify who can access which services and resources, and under which conditions.
With IAM policies, you manage permissions to your workforce and systems to ensure least-privilege permissions.

{{< img src="images/iam_simplified.png" height="90%" width="90%" align="center" title="iam" >}}

You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources.

A policy is an object in AWS that, when associated with an identity or resource, defines their permissions.
AWS evaluates these policies when a principal uses an IAM entity (user or role) to make a request.

Permissions in the policies determine whether the request is allowed or denied.



{{< vs 4 >}}

### Components

The main IAM components are:

- IAM Users - End users who log into the console or interact with AWS resources programmatically
- IAM Groups - Group up your Users so they all share permission levels of the group eg. Administrators, Developers, Auditors
- IAM Roles - Associate permissions to a Role and then assign this to Users or Groups Services
- IAM Policies - JSON documents which grant permissions for a specific user, group, or role to access services. Policies are attached to IAM Identities.

Roles can be applied to AWS Directory Service groups to quickly add and remove permissions to users.
The roles can have many policies attached.

A user can have a role directly attached A policy can be directly attached to a user (called an Inline Policy)

{{< vs 4 >}}

### Policies

##### Indentity-based


Identity-based policies are permissions policies that you attach to an IAM identity, such as an IAM user, group, or role.
It controls what actions the identity can perform, on which resources, and under what conditions.

{{< img src="images/policies.png" height="50%" width="50%" align="center" title="policies" >}}

Can be further categorized:

- AWS managed policies – Managed policies that are created and managed by AWS.
- Customer managed policies – Managed policies that you create and manage in your AWS account.
Customer managed policies provide more precise control over your policies than AWS managed policies.
- Inline policies – Policies that you create and manage and that are embedded directly into a single user, group, or role.

{{< alert type="warning" >}}
It's not recommend to use inline policies in most cases.
{{< /alert >}}

{{< vs 1 >}}

##### Resource-based

It controls what actions a specified principal can perform on that resource and under what conditions.
Basically it is a set of permissions that you attach to a resource such as an Amazon S3 bucket or an IAM role trust policy.

{{< alert type="info" >}}
Resource-based policies are inline policies, and there are no managed resource-based policies.
{{< /alert >}}

{{< vs 4 >}}
### Best Practices

The AWS has a guide showing up the best security practices to manage permission:
- Lock away the AWS account root user access keys
- Use roles to delegate permissions
- **Grant least privilege**
- Use customer managed policies instead of inline policies
- Use access levels to review IAM permissions
- Configure a strong password policy for users
- **Enable MFA**
- Use roles for applications that run on Amazon EC2 instances
- Do not share access keys
- **Rotate credentials regularly**
- Remove unnecessary credentials
- Use policy conditions for extra security
- Monitor activity in the AWS account

All tips are important, but for me the Grant least privilege is the most one.
It's because is a standard security advice of granting least privilege, or granting only the permissions required to perform a task.
That's way more secure than starting with permissions that are too lenient and then trying to tighten them later.

{{< alert type="info" >}}
For more information about the practices, check it out: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
{{< /alert >}}

{{< vs 4 >}}
### References
- Main AWS page: https://aws.amazon.com/iam/
- ABAC: https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_attribute-based-access-control.html
- Grant Least: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html