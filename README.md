## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://github.com/zacharycook1600/CS-Bootcamp-Project1/blob/main/Network%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions may be used to install only certain pieces, such as Filebeat.


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting access to the network, thereby limiting and mitigating potential security vulnerabilities.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for traffic anomoilies, allowing them to watch for potential malicious activity.


The configuration details of each machine may be found below.


| Name       | Function       | IP Address | Operating System |
|------------|----------------|------------|------------------|
| Jump-Box   | Gateway        | 10.0.0.9   | Linux            |
| Web-1      | DVWA Webserver | 10.0.0.10  | Linux            |
| Web-2      | DVWA Webserver | 10.0.0.12  | Linux            |
| Web-3      | DVWA Webserver | 10.0.0.14  | Linux            |
| Elk-Server | ELK Server     | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address: 69.255.45.REDACTED

Machines within the network can only be accessed through the Jump-Box machine via port 22 and SSH. However, the Elk-Server may accessed through port 5601 through its own public IP address (20.44.125.232) by its Kibana application.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump-Box   | Yes                 | 69.255.45.REDACTED   |
| Elk-Server | Yes                 | 69.255.45.REDACTED   |
| Web-1      | No                  | N/A                  |
| Web-2      | No                  | N/A                  |
| Web-3      | No                  | N/A                  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows the exact same configuration to be pushed out to every machine that the user chooses with one command.


The playbook implements the following tasks:
- Docker.io
- Increase virtual memory
- Install pip3
- Install docker python module
- Download and lauch a docker web container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://github.com/zacharycook1600/CS-Bootcamp-Project1/blob/main/docker%20ps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.10)
- Web-2 (10.0.0.12)
- Web-3 (10.0.0.14)

We have installed Filebeat on Web-1, Web-2, and Web-3. This will facilitate monitoring for any malicious activity in one central place. Filebeat was installed by using an ansible playbook, which may be easily edited in order to add or remove machines. Other playbooks can be created to implement similar security measures for the VMs in our resource group. 

These Beats allow us to collect information from each machine, including data on ssh attempts, system login events, and sudo commands. Filebeat puts all of this information into a dashboard that allows us to quickly analyze activity. See below for an example: 

![image](https://github.com/zacharycook1600/CS-Bootcamp-Project1/blob/main/Kibana_Dashboard.PNG)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat_configuration.yml file to the ELK VM.
- Update the hosts file to include 10.0.0.10, 10.0.0.12, and 10.0.0.14
- Run the playbook, and go to Kibana (20.44.125.232:5601) to confirm that the installation was correctly executed. 



