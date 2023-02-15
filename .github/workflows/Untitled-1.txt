#!/bin/bash

# Step 1: Setup your environment
export AWS_ACCESS_KEY_ID="<YOUR_KEY>"
export AWS_SECRET_ACCESS_KEY="<YOUR_SECRET_KEY>"
export AWS_DEFAULT_REGION="<YOUR_REGION>"

# Step 2: Spin up an EC2 instance
aws ec2 run-instances --image-id ami-027e5d5ba5f5ceb45 --count 1 --instance-type t2.micro --key-name <YOUR_KEYNAME> 

# Step 3: Install dependencies
sudo apt-get update && sudo apt-get install -y python python-pip unzip

# Step 4: Install kubectl
curl -o kubectl https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

# Step 5: Install Terraform
wget https://releases.hashicorp.com/terraform/0.11.13/terraform_0.11.13_linux_amd64.zip
unzip terraform_0.11.13_linux_amd64.zip
sudo mv terraform /usr/local/bin/

# Step 6: Install Jenkins
sudo apt-get install default-jdk -y
wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins -y 
