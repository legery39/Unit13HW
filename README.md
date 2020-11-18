# Unit13HW
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Update the path with the name of your diagram](Images/RedTeam_Security_Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

my_playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting external traffic to the network.
What aspect of security do load balancers protect? The load balancer defends an organization against distributed denial-of-service (DDoS) attacks. The load balancer actively defends against DDoS by shifting attack traffic from the corporate server to a public cloud provider.

What is the advantage of a jump box? The jump box allows the system to have fewer hardware resources and prevents to overuse of memory in cloud space.
 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network, containers and system performance.
What does Filebeat watch for?  Filebeat monitors for changes in the log files or locations that are specified and collects log events. 
What does Metricbeat record? Statics and metrics of operating system

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web1     | Internal | 10.0.0.5   | Linux            |
| Web2     | Internal | 10.0.0.8   | Linux            |
| Web3     | Internal | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
10.0.0.5
10.0.0.8
10.0.0.6

Machines within the network can only be accessed by Jumpbox.
Which machine did you allow to access your ELK VM? Jumpbox 
What was its IP address? 52.240.54.165

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses               |
|----------|---------------------|------------------------------------|
| Jump Box | Yes                 | 10.0.0.5 10.0.0.6 10.0.0.8         |
| Elk VM   | Yes                 | 10.0.0.4 10.0.0.5 10.0.0.8 10.0.0.6|
|          |                     |                                    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible? The advantage is to create an automated process of using one ansible machine to configure multiple machines. It also increases efficiency, security and allows the administrator to focus on more important tasks.

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Sets the host where the playbook will initiate.
- Prepares the remote user to access the Elk Server.
- Updates the system
- Installs python3-pip
- Installs docker module
- Increases memory and sets memory of container
- Downloads the container to Elk Server
- Opens ports 5601 & 9200 to listen for Kibana access

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Red-TeamWeb1 - 10.0.0.5 Red-TeamWeb2 - 10.0.0.8 Red-TeamWeb3 - 10.0.0.6

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat - monitors files we specify and creates a log whenever differences are detected.
Metricbeat - monitors the performance on the machines being monitored.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat config file to ansible directory.
- Update the hosts file to include...
- Run the playbook, and navigate to the Filebeat installation to check that the installation worked as expected.

- Which file is the playbook? myplaybook.yml, filebeat-playbook.yml, metricbeat-playbook.yml Where do you copy it? /etc/ansible/ inside the Ansible Docker Container
- Which file do you update to make Ansible run the playbook on a specific machine? Hosts File How do I specify which machine to install the ELK server on versus which to install Filebeat on? You modify the Filebeat-config.yml and the   metricbeat-config.yml with the machine ip address as well as the address for the Elk server. Also in both (Filebeat and Metricbeat) you place the name of the Elk server as the host.
- Which URL do you navigate to in order to check that the ELK server is running? http://137.116.52.192:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
-sudo docker container list -a
-sudo docker start focused_margulis
-sudo docker ps
-sudo docker attach focused_margulis
-cd /etc/ansible
-nano hosts
-nano my_playbook.yml
-ansible-playbook /etc/ansible/my_playbook.yml
-curl localhost/setup.php
-touch /etc/ansible/install-elk.yml
-touch /etc/ansible/filebeat-playbook.yml
-ansible-playbook /etc/ansible/filebeat-playbook.yml
-touch metricbeat-playbook.yml
-touch /etc/ansible/metricbeat-config.yml
-ansible-playbook /etc/ansible/metricbeat-playbook.yml
