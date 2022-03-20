# aws-ansible
Automated setup of EC2s, load balancers, and security groups.

## About

For my software defined networking class, we were tasked with automating the deployment of internet infrastructure using Ansible. We were given the choice to use any environment and any set of devices, so the project was self-directed in terms of what was built. I chose to use AWS and automate the deployment of EC2 webservers, a security group, and a load balancer. I automated the placement of the EC2s in the security and attached them to the load balancer, and also included a bootstrapped configuration of the EC2 webservers as part of the ansible script. No further configuration was needed beyond running my Ansible playbooks to get this up and running.

## Topology

Please excuse my graphic design skills... :)


!(https://i.imgur.com/gchQMb2.png)
