## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_projects.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - Enter the playbook file. filebeat-playbook.yml install-elk.yml 

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- What aspect of security do load balancers protect? Availability, Web Traffic, Web Security What is the advantage of a jump box? Automation, Security, Network Segmentation, Access Control

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- _TODO: What does Filebeat watch for?_ Log files or locations that you specify, collects log events anf forwards to logtash or elasticsearch
- _TODO: What does Metricbeat record?_  Takes the metrics and statistics that it collects and ships them to the output that you specify,

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1     |Webserver  10.0.0.5     Linux   |            |                  |
| Web-2    | Webserver  10.0.0.6     Linux   |            |                  |
  ELK-Server Monitoring 10.1.0.5 |   Linux         |            |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_ 		
172.58.28.26

Machines within the network can only be accessed by workstation and Jump-Box-Provisioner.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address? Jump-Box-Provisioner 10.0.0.4 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes              | 172.58.28.26
| DVWA-VM1   No   |             10.0.0.4                           
| DVWA-VM2   No   |             10.0.0.4                           
|ELKserver   No                 10.0.0.4

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because servcies running can be limited, system installation and update can be streamlined, and processes become more replicable
- _TODO: What is the main advantage of automating configuration with Ansible? Advantage is that you can put commands into multiple servers from a single playbook

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

- ...     #Use apt module
    - name: Install docker.io
      apt:
        update_cache: yes
        force_apt_get: yes
        name: docker.io
        state: present

- ...   # Use apt module
    - name: Install python3-pip
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present
- 
... # Use pip module (It will default to pip3)
    - name: Install Docker module
      pip:
        name: docker
        state: present

- ...
      # Use command module
    - name: Increase virtual memory
      command: sysctl -w vm.max_map_count=262144

- ...   # Please list the ports that ELK runs on
        published_ports:
          -  5601:5601
          -  9200:9200
          -  5044:5044



The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: Web 1 10.0.0.5 Web 2 10.0.0.6

We have installed the following Beats on these machines:ELK Server, Web1 and Web2
- _TODO: Specify which Beats you successfully installed_  FileBeat 

These Beats allow us to collect the following information from each machine:Filebeat: log events
Metricbeat: metrics and system statistics 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the  playbook file to /etc/ansible/roles.
- Update the host file to include webserver and elk
- Run the playbook, and navigate to Kibana  to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook?filebeat-playbook.yml  Where do you copy it?_ /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine? /etc/ansible/hosts How do I specify which machine to install the ELK server on versus which to install Filebeat on? I have to specify two separate groups in the etc/ansible/hosts file. One of the groups will be webservers which has the IPs of the VMs that I will install Filebeat to. The other group is named elkservers which will have the IP of the VM I will install ELK to. 

- _Which URL do you navigate to in order to check that the ELK server is running? 
20.150.136.47:6601/app/kibana 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._