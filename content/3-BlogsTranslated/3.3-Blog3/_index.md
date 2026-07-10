---
title: "Blog 3"
date: 2026-07-08
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Strengthening AWS Management Console Security with Sign-in Resource-based Policies and RCPs

Hello everyone in the AWS Study Group VN community!

AWS has recently introduced a new feature that strengthens the security of the AWS Management Console and AWS CLI through Sign-in Resource-based Policies and Resource Control Policies (RCPs).

This solution allows organizations to permit users to sign in to AWS only from trusted networks, reducing the risk of unauthorized access and helping meet security requirements.

In this article, we will explore:

- how Sign-in Resource-based Policies work
- how RCPs help manage access centrally
- the benefits of this approach for businesses

## 1. What are Sign-in Resource-based Policies?

Previously, login control was usually based on IAM or authentication policies. With this new feature, AWS allows policies to be applied directly during the sign-in process, helping control the access source before a user can enter the AWS Management Console.

For example, an organization can allow sign-in only from:

- the company’s internal network
- the enterprise VPN
- a specified Amazon VPC

Any request coming from the public internet or from unapproved locations will be denied at the sign-in step.

## 2. How RCPs help with centralized management

When using AWS Organizations, Resource Control Policies (RCPs) make it possible to apply the same security rule across many AWS accounts.

This helps organizations maintain a consistent network perimeter, reduce configuration errors, and ensure all accounts follow the same security policy.

## 3. Key benefits

This new solution offers several important advantages:

- only trusted networks are allowed to sign in
- reduces the risk of access from public Wi-Fi or unmanaged devices
- allows designated administrative accounts to remain accessible to avoid lockout
- records successful and denied sign-in attempts through AWS CloudTrail, which supports auditing and compliance

## Conclusion

With Sign-in Resource-based Policies and Resource Control Policies, AWS adds another layer of protection at the sign-in stage, allowing organizations to control access to the AWS Management Console more strictly.

Combined with AWS Organizations, AWS CloudTrail, and other security services, this solution helps:

- strengthen AWS account security
- establish an effective network perimeter
- manage policies centrally across many accounts
- support auditing and compliance requirements

For businesses operating workloads on AWS, this is a new feature worth considering to improve the safety of the cloud environment.

Source: https://aws.amazon.com/vi/blogs/security/restrict-aws-management-console-access-to-expected-networks-with-sign-in-resource-based-policies-and-rcps/
