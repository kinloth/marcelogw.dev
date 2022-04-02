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
With IAM policies, you manage permissions to your workforce and systems to ensure the least privilege permissions.

{{< img src="images/iam_simplified.png" height="90%" width="90%" align="center" title="iam" >}}

You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources.

A policy is an object in AWS that, when associated with an identity or resource, defines its permissions. AWS evaluates these policies when a principal uses an IAM entity (user or role) to make a request.

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

##### Identity-based

Identity-based policies are permissions policies that you attach to an IAM identity, such as an IAM user, group, or role.
It controls what actions the identity can perform, on which resources, and under what conditions.

{{< img src="images/policies.png" height="50%" width="50%" align="center" title="policies" >}}

Can be further categorized:

- AWS managed policies – Managed policies that are created and managed by AWS.
- Customer managed policies – Managed policies that you create and manage in your AWS account.
It provide more precise control over your policies than AWS-managed policies.
- Inline policies – Policies that you create and manage and that are embedded directly into a single user, group, or role.

{{< alert type="warning" >}}
It's not recommended to use inline policies in most cases.
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

{{< alert type="info" >}}
For more information about the practices, check it out: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
{{< /alert >}}

{{< vs 2 >}}

#### Grant least privilege
The Grant least privilege is one of the most important security best practices.
It's also known as *Principle of Least Privilege*, and was described as a design principle about 50 years ago:

> Least privilege: Every program and every user of the system should
operate using the least set of privileges necessary to complete the job.
Primarily, this principle limits the damage that can result from an accident or
error. It also reduces the number of potential interactions among privileged
programs to the minimum for correct operation, so that unintentional,
unwanted, or improper uses of privilege are less likely to occur. Thus, if a
question arises related to misuse of a privilege, the number of programs that
must be audited is minimized. Put a nother way, if a mechanism can provide
‘firewalls,’ the principle of least privilege provides a rationale for where to
install the firewalls. The military security rule of ‘need-to-know’ is an
example of this principle.
>
> --- *Jerry Saltzer and Mike Schroeder*

That’s way more secure than starting with permissions that are too lenient and then trying to tighten them later.
The AWS uses this principle: initially, every user(unless the root user) does not have any kind of permission, and it needs to be added (through policies) to be able to use the AWS services.


{{< vs 2 >}}
#### ABAC
**Attribute-based access control (ABAC)**, also known as policy-based access control for IAM, defines an access control paradigm whereby access rights are granted to users through the use of policies which combine <mark>attributes</mark> together.
In an ABAC environment, when a user logs in, the system grants or rejects access based on different attributes.

These attributes can be related to the:
- User
- Environment
- Accessed resource

{{< alert type="info" >}}
The policies can use any type of attributes (user attributes, resource attributes, object, environment attributes etc).
{{< /alert >}}

In AWS, these attributes are called tags.

Tags can be attached to IAM resources, including IAM entities (users or roles) and AWS resources.

These ABAC policies can be designed to allow operations when the principal's tag matches the resource tag.

For example:
We can have a tag `project="star-wars"` on S3 storage, DynamoDB Table, and the team trustworthy (group of users) for the project.
Behind that, simply create a policy that allows access when the role and the resource are tagged for the same value for `project`.

{{< alert type="success" >}}
ABAC is helpful in environments that are growing rapidly and help with situations where policy management becomes cumbersome.
{{< /alert >}}

{{< vs 4 >}}
### References
- Main AWS page: https://aws.amazon.com/iam/
- ABAC: https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_attribute-based-access-control.html
- ABAC Wiki: https://en.wikipedia.org/wiki/Attribute-based_access_control
- Best practices: https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
- Least Privilege and More: http://www.cs.cornell.edu/fbs/publications/leastPrivNeedham.pdf
- Attribute based access control: https://en.wikipedia.org/wiki/Attribute-based_access_control