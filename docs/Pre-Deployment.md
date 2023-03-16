# Phase 1 - Pre-Deployment
In this phase, we will create the EC2 instances and create Global and Golden AMIs.

## Pre-Deployment

### Create Golden AMI
A Golden AMI is a modified image created from a base AMI EC2 instance after installing required patches, updates and so>instances which will then include all the updates and changes made by the user. To create a Golden AMI, we first create>
Linux 2.                                                                                                                
- Install AWS CLI
- Install AWS CloudWatch Agent
- Install AWS SSM Agent

### Create Golden AMI for NGINX
On top of having our previous 3 software installed, this AMI will have further NGINX packages and it's dependencies ins>                                                                                                                        
- Install NGINX                                                                                                     
- Push custom memory metrics to CloudWatch Agent

### Create Golden AMI for Apache Tomcat
This Golden AMI will have Tomcat and all the dependencies installed and configured.

- Install Tomcat
- Configure Tomcat as a systemd service
- Install JDK 11
- Push custom memory metrics to CloudWatch Agent

### Create Golden AMI for Apache Maven Build Tool
This Golden AMI will have the Apache Maven Build Tool installed and configured to go.

- Install Maven
- Install Git
- Install JDK 11
- Add Maven Home to system PATH variable
