# Deploying a Java Web Application on AWS 3-Tier Architecture
This is an implementation of the original project challenge posted [here](https://devopsrealtime.com/deploy-java-application-on-aws-3-tier-architecture/)

## Goal
To deploy a highly scalable, secured and highly available Java Web Application using the AWS 3-Tier architecture and provide access from to end users from the public 
internet.

## Outline
[Create Global AMI](#create-global-ami)
[Create Golden AMI for NGINX](#create-golden-ami-for-nginx)
[Create Golden AMI for Apache Tomcat](#create-golden-ami-for-apache-tomcat)
[Create Golden AMI for Apache Maven Build Tool](#create-golden-ami-for-apache-maven-build-tool)
[VPC Deployment And Bastion Host](#vpc-deployment-and-bastion-host)
[Maven Build](#maven-build)
[AWS 3-Tier Architecture](#aws-3-tier-architecture)
[Database (RDS)](#database)
[Tomcat](#tomcat)
[NGINX](#nginx)
[Application Deployment](#application-deployment)
[Post Deployment](#post-deployment)
[Validation & Cleanup](#validation-and-cleanup)

## Details
### Create Global AMI
- Install AWS CLI
- Install AWS CloudWatch Agent
- Install AWS SSM Agent
### Create Golden AMI for NGINX
- Install NGINX
- Push custom memory metrics to CloudWatch Agent
### Create Golden AMI for Apache Tomcat
- Install Tomcat
- Configure Tomcat as a systemd service
- Install JDK 11
- Push custom memory metrics to CloudWatch Agent
### Create Golden AMI for Apache Maven Build Tool
- Install Maven
- Install Git
- Install JDK 11
- Add Maven Home to system PATH variable
### VPC Deployment and Bastion Host
### Maven Build
### AWS 3-Tier Architecture
####Database
####Tomcat
####NGINX
### Application Deployment
### Post Deployment
### Validation and Cleanup


