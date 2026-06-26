# Week 01 - AWS Cloud Networking Foundations

## Objective

Build and explain a basic AWS VPC network with public and private subnets, route tables, Internet Gateway, NAT Gateway, Security Groups and Network ACLs.

## Architecture Overview

This lab simulates a basic cloud network for a secure application environment.

The design includes:

- One VPC.
- Two public subnets.
- Two private subnets.
- One Internet Gateway.
- One public route table.
- One private route table.
- One bastion EC2 instance in a public subnet.
- One private EC2 instance in a private subnet.
- Controlled SSH access.
- Optional NAT Gateway for outbound internet access from private workloads.

## CIDR Plan

| Network | CIDR | Purpose |
|---|---|---|
| VPC | 10.10.0.0/16 | Main cloud network |
| public-a | 10.10.1.0/24 | Public subnet in AZ A |
| public-b | 10.10.2.0/24 | Public subnet in AZ B |
| private-a | 10.10.11.0/24 | Private subnet in AZ A |
| private-b | 10.10.12.0/24 | Private subnet in AZ B |

## Security Goals

- Only the bastion host should be reachable from the internet.
- SSH to the bastion must be restricted to my trusted public IP.
- Private EC2 instances must not have public IP addresses.
- Private EC2 instances should only accept SSH from the bastion Security Group.
- Private subnets should not have direct routes to the Internet Gateway.
- NAT Gateway should only be used to allow outbound internet access from private subnets.

## Public vs Private Subnets

A public subnet has a route to an Internet Gateway.

A private subnet does not have a direct route to an Internet Gateway. It can access the internet only through NAT if outbound connectivity is required.

## Route Tables

Public route table:


10.10.0.0/16 -> local
0.0.0.0/0    -> Internet Gateway

Private route table before NAT:


10.10.0.0/16 -> local


Private route table after NAT:


10.10.0.0/16 -> local
0.0.0.0/0    -> NAT Gateway


## Internet Gateway

An Internet Gateway allows resources in public subnets to communicate with the internet when routing, public IP assignment, Security Groups and Network ACLs allow it.

## NAT Gateway

A NAT Gateway allows private instances to initiate outbound connections to the internet without allowing unsolicited inbound connections from the internet.

## Security Groups vs Network ACLs

Security Groups are stateful and work at the instance or resource level.

Network ACLs are stateless and work at the subnet level.

| Control | Level | Stateful | Allows Deny Rules | Common Use |
|---|---|---:|---:|---|
| Security Group | Instance/resource | Yes | No | Primary access control |
| Network ACL | Subnet | No | Yes | Additional subnet guardrail |

## Connectivity Tests

Pending.

## Issues Found

Pending.

## Lessons Learned

Pending.

## Interview Questions

1. What makes a subnet public in AWS?
2. What is the difference between a Security Group and a Network ACL?
3. Why should databases usually be placed in private subnets?
4. Can an EC2 instance in a private subnet access the internet? How?
5. Why is `0.0.0.0/0` dangerous in inbound Security Group rules?
6. What is the purpose of an Internet Gateway?
7. What is the purpose of a NAT Gateway?
8. Why should SSH access be restricted to a trusted IP?
9. What happens if a private subnet route table has no default route?
10. How would you troubleshoot an EC2 instance that cannot access the internet?

## English Summary

Pending.