---
title: "Cognito"
date: 2022-04-02
description: AWS Cognito
hero: "images/hero.png"
menu:
  sidebar:
    name: Cognito
    identifier: aws-cognito
    parent: aws
    weight: 10
tags: ["AWS", "Storage", "Cloud", "Cognito"]
categories: ["AWS", "Cognito"]
---

### About

AWS Cognito is a service to handle user authentication and authorization.
Using the best security practices gives us the way to manage users and access.

It offers:
- Secure and scalable identity store
- Social and enterprise identity federation
- Standards-based authentication
- Security for apps and users
- Access control for AWS resources
- Easy integration with apps


{{< alert type="success" >}}
Cognito it’s cheap as well, with a free tier that gives 50,000 monthly active users for UserPools and 50 for users from SAML 2.0 based identity providers.
{{< /alert >}}

{{< vs 4 >}}
### Core Components

#### Cognito User Pool
Probably the most used feature, it offers a base of users to handle.
It contains a bunch of cool features to sign in and sign-up users, like MFA, password minimal requirements, account validation, etc.

{{< img src="images/userpool.png" height="70%" width="70%" align="center" title="userpool" >}}

{{< alert type="info" >}}
It’s possible to update increment behaviors (like adding more information to tokens) in most Cognito steps.
This can be accomplished by invoking lambdas after/before the steps.
{{< /alert >}}

{{< vs 2 >}}
#### Cognito Identity Pool
Provide temporary credentials for users to access AWS services, like S3, DynamoDB, Cloudwatch, etc.

{{< img src="images/identitypool.png" height="85%" width="85%" align="center" title="identitypool" >}}

{{< vs 2 >}}
#### Cognito Sync
AWS service and client library that makes it possible to sync application-related user data across devices.

Synchronize user profile data across mobile devices and the web without using a backend application.

The client libraries cache data locally so that the applications can read and write data regardless of device connectivity status.

{{< vs 4 >}}
### Security best practices
It's recommended to enable multi-factor authentication (MFA) to a user pool to protect the user's identity.
MFA adds a second authentication factor so that the user pool doesn't rely solely on user name and password.

{{< alert type="info" >}}
It's possible to choose to use SMS text messages, or time-based one-time passwords (TOTP) as second factors to sign in the users.
{{< /alert >}}

Also, it's useful to enable adaptive authentication with its risk-based model to predict when might need another authentication factor.
User pool advanced security features include adaptive authentication and protections against compromised credentials.

{{< vs 4 >}}
### References
- Main AWS page: https://aws.amazon.com/cognito/
- Sync: https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-sync.html
- Best Practices: https://docs.aws.amazon.com/cognito/latest/developerguide/managing-security.html