# aws-ansible
This project automates the setup of EC2s, load balancers, and security groups.

## About

For my software defined networking class, we were tasked with automating the deployment of internet infrastructure using Ansible. We were given the choice to use any environment and any set of devices, so the project was self-directed in terms of what was built. I chose to use AWS and automate the deployment of EC2 webservers, a security group, and a load balancer. I automated the placement of the EC2s in the security and attached them to the load balancer, and also included a bootstrapped configuration of the EC2 webservers as part of the ansible script. There are also scripts to gather facts about devices after they are configured. No further configuration was needed beyond running my Ansible playbooks to get this up and running.

## Topology

Please excuse my graphic design skills... :)


![GitHub Logo](https://i.imgur.com/gchQMb2.png)

## AWS Setup

This first part of the process is to prepare an AWS environment so that it can be managed through an ansible control node. Here are the steps:
1.	Create a new AWS account, outside of the learner academy. The AWS academy accounts do not have permissions to create IAM roles, so I created a new account with full permissions
2.	Create an EC2 instance on the account to server as the Ansible control node.
3.	SSH into the control node and run the following commands to setup ansible:
The EC2 control node now has everything installed that we need to for using it to manipulate AWS resources.
4.	We need to give the control node permissions to configure EC2s. Navigate to IAM on the AWS console, and create a new role.
5.	Give the new role the permission AmazonEC2FullAccess
6.	Attach the role to the EC2 instance that is serving as the ansible control node.

## Files

create_structures.yml - This file is the main playbook, and it creates the EC2s, load balancer, and security group.
user_data.sh - shebang script used by create_structures.yml to bootstrap the EC2 instances as webservers
gather_facts.yml - gathers facts about the configured AWS devices, and calls gather_info.py to use a boto3 script to gather information and print the output in a clean format :)
hosts - sets localhost as the host

## Running the playbooks

Run create_structures.yml with ansible, and specify the hosts file as the inventory.
Run gather_facts.yuml with ansible to output information about the devices configured with the playbook.

## Verify

Visit the DNS address of the load balancer. You will be brought to the index page of the one of web servers, which displays the IP address of the specific web server. Upon reload of the load balancer, you should be brought to a different web server, which we can tell from the change in IP address on the index page. Let's try it:

Visit 1:

![GitHub Logo](https://i.imgur.com/bmDr7Dn.png)

Visit 2:

![GitHub Logo](https://i.imgur.com/Fexl1Na.png)

Visit 3:

![GitHub Logo](https://i.imgur.com/ROBuA0g.png)

Gathering facts about EC2s with the boto3 script:

![GitHub Logo](https://i.imgur.com/smf3eEq.png)

