# Deploying a Java Web Application on AWS 3-Tier Architecture
This is an implementation of the original project challenge posted [here](https://devopsrealtime.com/deploy-java-application-on-aws-3-tier-architecture/)

# Goal
To deploy a highly scalable, secured and highly available Java Web Application using the AWS 3-Tier architecture and provide access from to end users from the public 
internet.

# Outline
- [Pre-Deployment](#pre-deployment)
  + [Create Global AMI](#create-global-ami)   
  + [Create Golden AMI for NGINX](#create-golden-ami-for-nginx)  
  + [Create Golden AMI for Apache Tomcat](#create-golden-ami-for-apache-tomcat)  
  + [Create Golden AMI for Apache Maven Build Tool](#create-golden-ami-for-apache-maven-build-tool)  
- [VPC Deployment And Bastion Host](#vpc-deployment-and-bastion-host)  
- [Maven Build](#maven-build)  
- [AWS 3-Tier Architecture](#aws-3-tier-architecture)  
  + [Database (RDS)](#database)  
  + [Tomcat](#tomcat)  
  + [NGINX](#nginx)  
- [Application Deployment](#application-deployment)  
- [Post Deployment](#post-deployment)  
- [Validation & Cleanup](#validation-and-cleanup)  

# Details

## Pre-Deployment

### Create Golden AMI
A Golden AMI is a modified image created from a base AMI EC2 instance after installing required patches, updates and software. This acts as a template to launch further 
instances which will then include all the updates and changes made by the user. To create a Golden AMI, we first create a base EC2 instance from an existing AMI like Amazon 
Linux 2.

:white_check_mark: Install AWS CLI

:white_check_mark: Install AWS CloudWatch Agent

:white_check_mark: Install AWS SSM Agent

:white_check_mark: Create new AMI based on this

### Create Golden AMI for NGINX
On top of having our previous 3 software installed, this AMI will have further NGINX packages and it's dependencies installed as a start.

:white_check_mark: Install NGINX

:white_check_mark: Push custom memory metrics to CloudWatch Agent

### Create Golden AMI for Apache Tomcat
This Golden AMI will have Tomcat and all the dependencies installed and configured.

:white_check_mark: Install Tomcat

:white_check_mark: Configure Tomcat as a systemd service

:white_check_mark: Install JDK 11

:white_check_mark: Push custom memory metrics to CloudWatch Agent

### Create Golden AMI for Apache Maven Build Tool
This Golden AMI will have the Apache Maven Build Tool installed and configured to go.

:white_check_mark: Install Maven

:white_check_mark: Install Git

:white_check_mark: Install JDK 11

:white_check_mark: Add Maven Home to system PATH variable

## VPC Deployment and Bastion Host
### VPC Setup
- [ ] Build VPC network ( 192.168.0.0/16 ) for Bastion Host deployment as per the architecture shown above.
- [ ] Build VPC network ( 172.32.0.0/16 ) for deploying Highly Available and Auto Scalable application servers as per the architecture shown above.
- [ ] Create NAT Gateway in Public Subnet and update Private Subnet associated Route Table accordingly to route the default traffic to NAT for outbound internet connection.
- [ ] Create Transit Gateway and associate both VPCs to the Transit Gateway  for private communication.
- [ ] Create Internet Gateway for each VPC and update Public Subnet associated Route Table accordingly to route the default traffic to IGW for inbound/outbound internet connection.

### Bastion Host Setup
- [ ] Deploy Bastion Host in the Public Subnet with EIP associated.
- [ ] Create Security Group allowing port 22 from public internet

## Maven Build
- [ ] Create EC2 instance using Maven Golden AMI
- [ ] Clone Bitbucket repository to VSCode and update the pom.xml with Sonar and JFROG deployment details.
- [ ] Add settings.xml file to the root folder of the repository with the JFROG credentials and JFROG repo to resolve the dependencies.
- [ ] Update application.properties file with JDBC connection string to authenticate with MySQL.
- [ ] Push the code changes to feature branch of Bitbucket repository
- [ ] Raise Pull Request to approve the PR and Merge the changes to Master branch.
- [ ] Login to EC2 instance and clone the Bitbucket repository
- [ ] Build the source code using  maven arguments "-s settings.xml"
- [ ] Integrate Maven build with Sonar Cloud and generate analysis dashboard with default Quality Gate profile.

## AWS 3-Tier Architecture
### Database
- [ ] Deploy Multi-AZ MySQL RDS instance into private subnets
- [ ] Create Security Group allowing port 3306 from App instances and from Bastion Host.

### Tomcat
- [ ] Create private facing Network Load Balancer and Target Group.
- [ ] Create Launch Configuration with below configuration.
  + [ ] Tomcat Golden AMI
  + [ ] User Data to deploy .war artifact from JFROG into webapps folder.
  + [ ] Security Group allowing Port 22 from Bastion Host and Port 8080 from private NLB.
- [ ] Create Auto Scaling Group

### NGINX
- [ ] Create public facing Network Load Balancer and Target Group.
- [ ] Create Launch Configuration with below configuration
  + [ ] Nginx Golden AMI
  + [ ] User Data to update proxy_pass rules in nginx.conf file and reload nginx service.
  + [ ] Security Group allowing Port 22 from Bastion Host and Port 80 from Public NLB.
- [ ] Create Auto Scaling Group

## Application Deployment
- [ ] Artifact deployment taken care by User Data script during  Application tier EC2 instance launch process.
- [ ] Login to MySQL database from Application Server using MySQL CLI client and create database and table schema to store the user login data (Instructions are update in README.md file in the Bitbucket repo)

## Post Deployment
- [ ] Configure Cronjob to push the Tomcat Application log data to S3 bucket and also rotate the log data to remove the log data on the server after the data pushed to S3 Bucket.
- [ ] Configure Cloudwatch alarms to send E-Mail notification when database connections are more than 100 threshold.

## Validation and Cleanup
- [ ] Verify you as an administrator able to login to EC2 instances from session manager & from Bastion Host.
- [ ] Verify if you as an end user able to access application from public internet browser.
- [ ] Remove all AWS resources
