# 🔐 Virtual Private Cloud - VPC

We need to understand the main concepts of the resources of VPC

- [VPC](#vpc)
- [Subnets](#subnets)
- [Internet Gateway](#internet-gateway)
- [NAT Gateway](#nat-gateway)
- [Security Groups]()
- [Network ACL (NACL)]()
- [VPC Flow Logs]()
- [VPC Peering]()
- [VPC Endpoints]()
- [Site to Site VPN]()
- [Direct Connect]()
- [Transit Gateway]()
- [Summary](#summary)

## VPC

VPC stands to Virtual Private Cloud and it is a private network to deploy your resources (regional resource). A VPC is linked to specific region, so we can have multiple VPC.

Inside of VPC we have Subnets and CIDR Ranges (allowed IPs)

Sample VPC example:

- We have the AWS Cloud, and AWS Has regions, inside that region we create a VPC. Inside the VPC we create the CIDR ranges to define the allowed IPs and the subnets.
- Our VPC can reach one or more AZs, so we have the subnets, each subnet inside an AZ. Inside Each Subnet, we have Public and Private subnets.
<center><img src="vpc-sample.jpg" alt="drawing" width="500"/></center>

## Subnets

Subnets are partition of our network and is associated to an Availability Zone

- **Public Subnet**: Is a subnet accessible for the internet (we can put, for example, an EC2 Instance). It requires an internet gateway.
- **Private Subnet**: Is a subnet not accessible for the internet (we can put, for example, a database). Our private subnet can have access to the internet by using the NAT Gateway.

To define access to the internet and communication between subnets, we use route tables.

## Internet Gateway

Inside each subnet we can have EC2 instances, For this instances be accessible to the internet, we need to use the Internet Gateway. The internet gateway create a way to our Subnet connect to the internet.

The public subnet will have a route to the internet gateway that is communicating with the internet. As soon we have the internet gateway and a route to it, that makes the subnet a **public subnet**

## NAT Gateway

Works with the **Private Subnet**. By default private subnet does not have access to the internet and cannot be accessed through the internet as well. But if we need to access the internet (for updates to softwares, or something similar) we can use the NAT Gateway.

NAT Gateway is a AWS-Managed service to allow private subnet access the internet while remaining private.

The NAT Gateway need to be created inside the Public Subnet and we create a Route from our Private Subnet to this NAT Gateway and it will be able to get internet connectivity.

### Using Internet and NAT Gateways

Following the same example of sample VPC:

- Inside each subnet we can have EC2 instances, and to allow the public subnet we create the Internet Gateway and create the route to it, and it goes to the internet.
- Inside the private subnet, by default we do not have access to the internet, so to get the access (to update a software into EC2), we need to create a NAT Gateway inside the Public Subnet and create a Route to this NAT Gateway. The NAT Gateway will communicate with Internet Gateway and the internet gateway will perform the access.
<center><img src="gateways.jpg" alt="drawing" width="300"/></center>

## Summary

[UP](#🔐-virtual-private-Cloud---vpc)