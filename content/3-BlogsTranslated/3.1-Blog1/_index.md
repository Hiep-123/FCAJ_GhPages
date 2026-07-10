---
title: "Blog 1"
date: 2026-07-08
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Building Dual-token Authentication for Nakama Game Servers with Amazon Cognito on AWS

Hello everyone in the AWS Study Group VN community!

Today I would like to share an interesting AWS architecture for multiplayer game systems that use **Nakama**.

In online games, managing **player accounts** and **in-game session connections** are often two separate problems. If they are not designed carefully, players may need to authenticate multiple times or experience interruptions when moving between services.

To solve this, AWS introduces a pattern called **Dual-token Authentication**, which combines **Amazon Cognito** and **Nakama** to provide both strong security and a seamless login experience.

This article will help us understand:

- what Dual-token Authentication is
- how the architecture works on AWS
- why this model is useful for multiplayer games

## 1. What is Dual-token Authentication?

Instead of using a single token for the entire system, this approach splits authentication into two stages.

First, **Amazon Cognito** verifies the player’s identity and issues a **JWT access token**. Then, when the player connects to **Nakama**, a **Go Runtime Hook** validates the JWT and creates a **session token** for the game session.

By separating the two token types, the system improves security while allowing players to sign in and join the game smoothly.

## 2. AWS architecture

To implement this solution, AWS combines several services that work together:

- **Amazon CloudFront** and **AWS WAF** protect the entry point and filter malicious traffic.
- **Application Load Balancer** and **Network Load Balancer** route requests to the appropriate services.
- **Amazon ECS** hosts the game services and Nakama runtime.
- **Amazon Cognito** handles identity and token issuance.
- **Nakama** uses the validated JWT to create a gameplay session token.

This creates a modern architecture that is both secure and scalable as the number of players grows.

![Kiến trúc tổng quan](/images/3-BlogsTranslated/3.1-Blog1/blog3_1.jpg)

## 3. Why this model stands out

One important point is that AWS uses both **ALB** and **NLB** rather than relying on a single load balancer.

All traffic still flows through **Amazon CloudFront**, so players only need one public endpoint while the platform internally routes requests to the appropriate service.

This design is especially useful for games that require:

- fast and secure authentication
- low-latency communication
- elastic scaling during traffic spikes

## Conclusion

Dual-token Authentication is a strong option for online game platforms on AWS. By combining **Amazon Cognito**, **Amazon CloudFront**, **AWS WAF**, **Application Load Balancer**, **Network Load Balancer**, and **Amazon ECS**, teams can build an architecture that balances security, performance, and user experience.

Source: https://aws.amazon.com/vi/blogs/architecture/dual-token-authentication-for-nakama-game-servers-with-amazon-cognito-on-aws/
