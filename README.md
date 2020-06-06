# ELK-PROJECT
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  -

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting unathorized accessing to the network.
-What aspect of security do load balancers protect? What is the advantage of a jump box?_It allows connectivity into the vitual network from external sources and hides internal machines by allowing connectivity via private addresses.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the container and system logs.
-What does Filebeat watch for? Watches system logs.
-What does Metricbeat record?_  It watches the ELK logs.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

Name	    Function	          ip address	OS
elk	      log aggregator	    10.1.1.2	ubuntu 18.04
dvwa1	    virtual machine	    10.0.1.2	ubuntu 18.04
dvwa2	    virtual machine	    10.0.1.3	ubuntu 18.04
dvwa3	    virtual machine	    10.0.1.4	ubuntu 18.04
jumpbox	  entry point gateway	10.0.1.5	ubuntu 18.04

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _Add whitelisted IP addresses (please see below chart)

Machines within the network can only be accessed by (please see below chart)
-Which machine did you allow to access your ELK VM? What was its IP address? (please see below chart)

A summary of the access policies in place can be found in the table below.

Name	  Publicly Accessible	  Allowed ip addresses
elk	    yes via port 9200	    From DVWA machines
dvwa1	  no	                  n/a
dvwa2	  no	                  n/a
dvwa3	  no	                  n/a
jumpbox	yes via ssh	          From home private IP


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? It reduces human error especially at scale and makes the job essier and faster. 

The playbook implements the following tasks:
-In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.

- ssh to jumpbox
- install docker.io
- pull Ansible container
- build and run ELK playbook
- configure security rules to allow inbound ports 9200,5601 Collapse

-
- 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)(see attached docker file)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring: 10.0.1.2- DVWA1, 10.0.1.3- DVWA2, 10.0.1.4- DVWA3

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed: Filebeat and Metricbeat_

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.  Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible playbook file to into the directories on dvwa and dvwa1 vm's.
- Update the playbook file to include metric beat and filebeat
- Run the playbook, and navigate to Elk Server to check that the installation worked as expected.

- Answer the following questions to fill in the blanks:_
- Which file is the playbook? ansible playbook.yml Where do you copy it? /etc/ansible/hosts 
- Which file do you update to make Ansible run the playbook on a specific machine? ansible.cfg How do I specify which machine to install the ELK server on versus which to install Filebeat on? vim install/elk.yml and vim install/filebeat.yml
- _Which URL do you navigate to in order to check that the ELK server is running? http://localhost:9200

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._To run; ansible-playbook elk-install.yml
