# ELK-stack-project1
Project1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](https://github.com/BMolina2022/ELK-stack-project1/blob/main/Images/ProjectDiagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _playbook____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._(https://github.com/BMolina2022/ELK-stack-project1/blob/main/yml-files/Elkplaybook.PNG)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly __available___, in addition to restricting _access____ to the network.
- _TODO: What aspect of security do load balancers protect?

A load balancer serves as a point of access for a service that is served by multiple machines. This allows for higher availability.

 What is the advantage of a jump box?_

A jump box serves as a gateway into a remote network, the main mode of access is usually SSH. Without the key one can not gain access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_

Filebeat is mainly used to watch system logs and forward any changesto the Elasticsearch host.

- _TODO: What does Metricbeat record?_

Metricbeat records metrics and provides system resources used for display in Elasticsearch

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     |  Function   | IP Address | Operating System |
|----------| ----------  |------------|------------------|
| JBoxVM   | Gateway     | 10.0.0.4   |  Linux           |
| Web1     |Web Server   | 10.0.0.5   |  Linux           |
| Web2     |Web Server   | 10.0.0.6   |  Linux           |
|ELK-Server|Elasticsearch| 10.1.0.4   |  Linux           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _Jump Box____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_

216.49.28.74

Machines within the network can only be accessed by _Jump Box____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
         
          JBoxVM 
          Public IP: 20.229.138.61
          Private IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JBoxVM   | SSH 22 Yes          | 216.49.28.74         |
| Web 1&2  | no                  |RedTeamLB: 13.80.19.7 |
|RedTeamLB | HTTP 80 yes         | *                    |
|ELK-Server| Kibana 5601 yes     | *                    |
|ELK-Server| HTTP 9200 yes       | 10.0.0.0/16          |




### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

It allows for full automation of a specific server and reduces configuration errors


The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

- Install Docker: Installs the core docker code to the remote server

- Install Python3_pip: Pip is an installation module that allows for additional docker modules to be installed easier

Docker Module: Tells the previous PIP module to install the necessary docker component modules
  Increase Memory/Use more memory: A common issue with the ELK Docker image is to little memory. This help fix the issue to allow the server to launch
  Download and launch ELK container: This downloads the ELK docker container and initializes it with the specified ports being published
  
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


![TODO: Update the path with the name of your screenshot of docker ps output](https://github.com/BMolina2022/ELK-stack-project1/blob/main/Images/sudo%20docker%20ps%20project1.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

10.1.0.4

10.0.0.4

10.0.0.5

10.0.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Filebeats collects system type events such as logins to see who is actively logging into the system.

Metricbeats collects useful information such as cpu usage and memory, this is particularly useful when seeing if there are any aberant programs or behaviors taking system resources.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __elk_install.yml___ file to __/etc/ansible/elk_install.yml___.
- Update the __hosts___ file to include...
the attribute, such as [elk], then include your destination ip of the ELK server directly below.

- Run the playbook, and navigate to _JBoxVM___ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_

elk-playbook.yml 

- _Which file do you update to make Ansible run the playbook on a specific machine?

elk-playbook.yml

 How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

By using the IPs of the respective servers.

- _Which URL do you navigate to in order to check that the ELK server is running?

http://[20.238.36.159]:5601/app/kibana
