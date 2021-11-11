# Elk-Stack-Project-1

Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![ElkDiagram](https://user-images.githubusercontent.com/85416113/141267339-434d45a5-5bd6-4eaf-ab25-103727416a9b.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

[Ansible Elk Playbook](https://github.com/kish-bot/Elk-Stack-Project-1/tree/main/Ansible)

This document contains the following details:

* Description of the Topology
* Access Policies
* ELK Configuration
  * Beats in Use
  * Machines Being Monitored
* How to Use the Ansible Build

## Description of the Topology**

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network. Load balancers protects the system from DDoS attacks by shifting attack traffic. The advantage of a jump box is to give access to the user from a single node that can be secured and monitored.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

Filebeat watches for any information in the file system which has been changed and when it has. Metricbeat takes the metrics and statistics that you collects and displays in a format of your choosing.

The configuration details of each machine may be found below.

Name | Function | IP Address | Os |Container Type | 
--- | --- | --- | --- | --- 
Jumpbox | Gateway | 10.0.0.8 | Linux | Ansible
Web1 | Web Server | 10.0.0.5 | Linux | DVWA
Web2 | Web Server | 10.0.0.6 | Linux | DVWA
Web3 | Web Server | 10.0.0.7 | Linux | DVWA

## Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the designated Admin's public IP address

Machines within the network can only be accessed by each other. Jump Box can SSH into the Web Servers and Elk Servers. Web Servers sent log information to the Elk Server

A summary of the access policies in place can be found in the table below.

Name | Publicly Accessible | Allowed IP Addresses
--- | --- | --- 
JumpBox | No | Admin Public IP Address
Web1 | Yes but only after whitelising the public IP | 10.0.0.8
Web2 | Yes but only after whitelising the public IP | 10.0.0.8
Web3 | Yes but only after whitelising the public IP | 10.0.0.8
Elk | No | Admin Machine Public IP Address and 10.0.0.8 

## Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, the main advantage of automating the installation process is that we could deploy multiple servers easily and quickly without having to physically touch each server.

The playbook implements the following tasks:

* Install Docker.io and pip3
* Increases VM memory
* Download and Configure elk docker container
* Sets Published Ports

## Target Machines & Beats

This ELK server is configured to monitor the following machines:

* 10.0.0.5
* 10.0.0.6
* 10.0.0.7

We have installed the following Beats on these machines:

* Filebeats
* Metricbeats

These Beats allow us to collect the following information from each machine:

* Filebeat collects log files and log events such as when someone attempts to elevate their permissions in a machine.
* Metricbeat collects data on the current condition of the OS and the services running on that OS such as the current amount of memory being used or the amount of storage left on the system as well as the amount of inbound and outbound data.

## Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned.

SSH into the control node and follow the steps below:

1. Copy the .yml files to `/etc/ansible` directory.
2. Update the hosts file to be as follows. This will assign the VM servers to their server groups for the Ansible Playbooks. 

```
[webservers]
10.0.0.5
10.0.0.6
10.0.0.7
[elkservers]
10.1.0.4
```   
3. Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.
```
cd /etc/ansible
ansible-playbook elk-playbook.yml
ansible-playbook filebeat-playbook.yml
ansible-playbook metricbeat-playbook.yml 
```
4. Then, run: `curl http://10.0.0.8:5601`. (You can also use the loadbalancer's public IP address) This is the address of Kibana. If the installation succeeded, this command should print HTML to the console.
