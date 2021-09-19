## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/Project 1 Network Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  install-dvwa.yml
  install-elk.yml
  filebeat-playbook.yml
  filebeat-config.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system services.

The configuration details of each machine may be found below.

| Name                 | Function   | IP Address | Operating System |
|----------------------|------------|------------|------------------|
| Jump Box Provisioner | Gateway    | 10.0.0.4   | Linux            |
| Web 1                | Web Server | 10.0.0.5   | Linux            |
| Web 2                | Web Server | 10.0.0.6   | Linux            |
| Project1 ELK         | Monitoring | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box and ELK machines can accept connections from the Internet. Access to these machines is only allowed from the following IP addresses: 206.198.179.195

Machines within the network can only be accessed by the Jump Box at 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump Box Provisioner | Yes                 | 206.198.179.195      |
| Project1-ELK         | Yes                 | 206.198.179.195      |
| Web 1                | No                  | 10.0.0.4             |
| Web 2                | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it makes this operation highly scalable.  It is very easy to add and setup new machines with this method as a business grows and needs expand.

The playbook implements the following tasks:
- Install Docker
- Install python
- Increase virtual memory
- Download ELK image
- Enable docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/Docker PS Output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web 1: 10.0.0.5
Web 2: 10.0.0.6

We have installed the following Beats on these machines:
Filebeat

These Beats allow us to collect the following information from each machine:
Filebeat allows us to easily read information from various files on the machine we are monitoring.  Specifically, it can be set up to monitor changes to system and application log files.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/hosts.
- Copy the filebeat-config.yml file to /etc/ansible/hosts/files.
- Copy the filebeat-playbook.yml file to /etc/ansible/hosts/roles.
- Update the /etc/ansible/hosts file to include the ip addresses of the machines you want to install ELK/Filebeat on and specify those to be in different groups. E.G.
	[webservers]
	10.0.0.5 ansible_python_interpreter=/usr/bin/python3
	[elk]
	10.1.0.4 ansible_python_interpreter=/usr/bin/python3
- Run the playbook, and navigate to http://[elk-VM-external-ip-address]:5601/app/kibana to check that the installation worked as expected.
	In this case the url is http://13.86.113.199:5601/app/kibana
