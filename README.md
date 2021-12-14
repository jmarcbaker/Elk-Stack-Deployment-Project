## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://drive.google.com/file/d/18hv4qLH38oovmE3za8zS8FzlJxJDv2Tp/view?usp=sharing

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  /etc/ansible/install-elk-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- What aspect of security do load balancers protect?
	
	- Load Balancers manage inbound traffic and distributes the traffic between available servers in an attempt to mitigate against denial of service attacks. By evenly distributing traffic, helps prevent any one server from being overloaded and potentially taken offline due to an influx of requests. 
	
- What is the advantage of a jump box?_
	- A jump box limits the access the general public has to the virtual network and the machines on that network. A user would need to gain the private IP addresses of the virtual machines in order to gain access thru the jump box.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- What does Filebeat watch for?
	- Filebeat monitors for changes in files and records those changes such as when and where the change occurred. Filebeat will collect log events and then index those files to be analyzed later.
	
-  What does Metricbeat record?
	- Metricbeat records statistics and metrics from the OS to monitor network servers running systems and services. Metricbeat can be installed on servers to periodically collect OS metrics.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.6   | Linux            |
|RedWeb1   |Web Server| 10.0.0.5   | Linux            |
|Redweb2   |Web Server| 10.0.0.7   | Linux            |
|ELK       |Log Server| 10.0.0.4   | Linux            |
 
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 76.27.178.183


Machines within the network can only be accessed by the Jump Box Provisioner.
-  Which machine did you allow to access your ELK VM?
	- Jump Box Provisioner

- What was its IP address?
	- 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              |76.27.178.183         |
| RedWeb1  | No                  |10.0.0.5              |
| RedWeb2  | No                  |10.0.0.7              |
| ELK      | Yes                 |10.0.0.4              |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-  What is the main advantage of automating configuration with Ansible?
	- Automating configuration with Ansible can be advantageous by removing the need to configure ELK manually, usage of playbooks written in YAML serve as a better alternative for configuration management and automation. These playbooks are also reusable for future configuration changes or updates.

The playbook implements the following tasks:
- The Elk playbook installs docker.io on the Elk vm.
- Python software is intalled on the Elk
- Virtual memory is increased to 262144 in order to operate Elk effectively
- Establishes the defined amount of memory to use when running Elk
- Downloads, installs, and executes the docker elk container on system restart.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- RedWeb1 - 10.0.0.5
- RedWeb2 - 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat, Metricbeat, and Packetbeat

These Beats allow us to collect the following information from each machine:
-Filebeat collects log data about the file system and highlights any changes to the file structure. More specifically Filebeat is used to collect Apache server logs.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

**Filebeat**
- Copy the filebeat-configuration.yml file to /etc/ansible/files/filebeat-config.yml.
- Update the filebeat-configuration.yml file file to include the private IP of the Elk machine on line(s)# 1106 & 1806.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

**Metricbeat**
- Copy the metricbeat-configuration.yml file to /etc/ansible/roles/files.
- Update the metricbeat-configuration.yml file to include the private IP address of the Elk machine on line(s)# 62 & 96.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

**Answer the following questions to fill in the blanks:_**
- Which file is the playbook? filebeat-playbook.yml Where do you copy it?  /etc/ansible/roles
- Which file do you update to make Ansible run the playbook on a specific machine?  filebeat-config.yml  
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
- Which URL do you navigate to in order to check that the ELK server is running? http://76.27.178.183:5601/app/Kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
 
 - To create or update yaml file: nano filebeat-playbook.yml
 - To run playbook: ansible-playbook filebeat-playbook.yml
 
