# Phase 2 - Network Setup
In this phase, we will setup the AWS networks and a Bastion Host.

## VPC Deployment and Bastion Host

### VPC Setup
- [ ] Build VPC network ( 192.168.0.0/16 ) for Bastion Host deployment as per the architecture shown above.
- [ ] Build VPC network ( 172.32.0.0/16 ) for deploying Highly Available and Auto Scalable application servers as per t>- [ ] Create NAT Gateway in Public Subnet and update Private Subnet associated Route Table accordingly to route the def>- [ ] Create Transit Gateway and associate both VPCs to the Transit Gateway  for private communication.                 - [ ] Create Internet Gateway for each VPC and update Public Subnet associated Route Table accordingly to route the def>                                                                                                                        

### Bastion Host Setup
- [ ] Deploy Bastion Host in the Public Subnet with EIP associated.
- [ ] Create Security Group allowing port 22 from public internet



---

[Phase 1: Pre-Deployment](/docs/1-pre-deployment.md)																																					[Phase 3: Maven Build](/docs/maven-build.md)
