# Phase 1 - Pre-Deployment
In this phase, we will create the EC2 instances and create Global and Golden AMIs.

## Pre-Deployment

### Create Golden AMI
A Golden AMI is a modified image created from a base AMI EC2 instance after installing required patches, updates and so>instances which will then include all the updates and changes made by the user. 

#### Create IAM Role

To install and use CloudWatch Agent, we will first need to enable a Role with a suitable policy before we initiate the EC2 instance.

1. Go to the IAM dashboard and click on '**Roles**'
2. Click on '**Create Role**'
3. In 'Trusted Entity Type', select '**AWS service**'
4. In the 'Use Case' section, under 'Common uses cases', select '**EC2**' and click next.
5. Search for and select '**CloudWatchAgentServerPolicy**'
6. Name your role as *CloudWatchAgentServerRole*

Now we can create our EC2 instance.

#### Launch EC2 Instance

From the EC2 console, launch a new EC2 instance. We are using an Ubuntu 20.04 AMI to do this. Once the instance is launched and running, we will attach an IAM role to it.

1. Select the EC2 instance
2. In the top right corner, go to Actions -> Security -> Modify IAM Role
3. From the dropdown, select the role we just created above, '**CloudWatchAgentServerRole**'
4. Click on Update Role.

#### Install AWS CLI

Before jumping ahead in installing AWS CLI, we will need to install 'unzip'. This will be used to unzip the official AWS CLI package.

```bash
sudo apt install unzip
```

We are using the official AWS [documentation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) to install AWS CLI. This method uses a download, extract and install procedure (which is why we installed unzip first).

 Once the process has completed, you can check the AWS version using

```bash
aws --version
```

![AWS Installed](images/pre-deployment/aws_installed.png)

#### Install AWS CloudWatch Agent

The next step is to install the AWS CloudWatch Agent. This is where we will push all of our custom memory metrics.

```bash
wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb

sudo dpkg -i -E ./amazon-cloudwatch-agent.deb
```

This will install the CloudWatch Agent. You need to check if it is running or not. In our case, after installing, it did not run automatically.

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status
```

![CloudWatch Agent Installed but Not Running](images/pre-deployment/cwa_installed_unstarted.png)

If it's running for you, move on. If not, then start the agent.

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -s -c ssm:configuration-parameter-store-name
```

#### Install AWS SSM Agent

First, we need to check if the SSM agent is pre-installed or not. As per the [AWS docs](https://docs.aws.amazon.com/systems-manager/latest/userguide/ami-preinstalled-agent.html), it should come pre-installed with our version of Ubuntu. Let's verify this

```bash
sudo systemctl status snap.amazon-ssm-agent.amazon-ssm-agent.service
```

![SSM Agent Running](images/pre-deployment/ssm_agent_running.png)

Once all these steps are finished, we are ready to create our Image from this instance.

1. In the EC2 dashboard, select the instance.
2. In the top right corner, click on Actions -> Image & Templates -> Create Image
3. Use any name you like. We will use '**Global_AMI**'
4. Keep all the default options and create the image.
5. In the left navigation, go to AMIs and you should see your newly created AMI.

> Note: It may take a while to be fully created. It will be in a '*pending*' state initially.

Now, every time you use this AMI to create an instance, it will come pre-installed with AWS CLI, CloudWatchAgent and SSM.

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
