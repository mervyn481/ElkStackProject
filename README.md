# ElkStackProject
Elk Stack Project.
 Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/mervyn481/ElkStackProject/blob/main/ELK%20STACK%20TOPOLOGY%202.png



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the [ .yml and .config ] file may be used to install only certain pieces of it, such as Filebeat.

  Enter the playbook file.
1] nano my-playbook.yml 
2] nano hosts
3] nano ansible.cfg
4] ansible elk installation and vm configuration
5] filebeat config
6] filebeat playbook - [enter link to filebeat-playbook.yml]
7] metricbeat config
8] metricbeat playbook

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly functional and available, in addition to restricting traffic to the network.
What aspect of security do load balancers protect?
 Load balancing distributes network traffic across multiple servers, which allows each server to operate without overloading and allows for switching out of any server that may be under cyber attack. This ensures availability of applications and websites for clients and end users.



What is the advantage of a jump box? 
A jump box is advantageous as a network security feature on the network because it acts as a source of protection for the VMs located behind it. The jump box allows a safe space for system configurations on the public side which can then be pushed securely  to the private secure VMs.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.

What does Filebeat watch for?
Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

What does Metricbeat record?
Metricbeat is a lightweight agent that can be installed on target servers to periodically collect metric data from your target servers, this could be operating system metrics such as CPU or memory or data related to services running on the server.
 [source: https://medium.com/devops-dudes/getting-started-with-metricbeat]

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.



Name
Function
IP Address private
IP Address public
Operating System


Jump Box
Gateway
10.1.0.4
20.222.104.28
Linux


VM2
Server
10.1.0.7
20.27.28.37
Linux


VM3
Server
10.1.0.8
20.27.28.37
Linux


ELK Server
Server
10.0.0.4
20.214.0.4
Linux





 Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box_Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 
My workstation using my public IP
 Add whitelisted IP addresses_ 20.222.104.28
[Note: The ELK server was also accessed from my workstation Chrome browser using public IP and port 5601]

Machines within the network can only be accessed by Workstation, Jump Box and ELK vm.
Which machine did you allow to access your ELK VM? Jump Box SSH port 22
What was its IP address? 10.1.0.4

A summary of the access policies in place can be found in the table below.


Name
Publicly Accessible
Allowed IP Addresses






Jump Box
Yes
20.222.104.28 SSH PORT 22






VM2
No
10.1.0.7 SSH PORT 22






VM3
No
10.1.0.8 SSH PORT 22






ELK Server
Yes
Workstation my public TPC 5601





















Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because…

What is the main advantage of automating configuration with Ansible?
Ansible allows for simple and rapid deployment of applications by using a yaml playbook.

The playbook implements the following tasks: 

Specify machine grouping:
Install Docker.io:
Install Python-pip
Increase Virtual Memory
Download/Launch ELK Docker Container [sebp/elk - image]
Published ports 5044, 5601 & 9200 made available:











The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)







Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring

VM2: 10.1.0.7
VM3: 10.1.0.8
We have installed the following Beats on these machines:
Specify which Beats you successfully installed:

Filebeat
Metricbeat 

These Beats allow us to collect the following information from each machine:

Filebeat is used to collect logs of various input types from the specified servers: Log, Syslogs, TCP, UDP,  etc
Examples are as follows: 

Log


Syslog


TCP 




UDP
 
 

Metricbeat is used to collect and monitor metrics such as stats fromCPU, memory, filesystems, network, data related to services running on a Targets server, etc.

Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

Answer the following questions to fill in the blanks:
Copy the filebeat-configuration.yml file and metricbeat-configuration.yml file to the ELM VM [etc/ansible/files]
Update the config file to include DVWA web servers 10.1.0.7, 10.1.0.8
Execute the playbook and check Kibana [elk-server-public IP:5601/app/kibana] to verify that installation was successful.
Which file is the playbook? 
Elk.playbook.yml - install ELK Server
Filebeat-playbook.yml -install and configure Filebeat on ELK and DVWA containers
Metricbeat-playbook.yml -install and configure Metricbeat on ELK and DVWA containers
 Where do you copy it? 
etc/ansible
 Which file do you update to make Ansible run the playbook on a specific machine? 
/etc/ansible/hosts.cfg
 How do I specify which machine to install the ELK server on versus which to install Filebeat on?
This is configured in etc/ansible/hosts 
Which URL do you navigate to in order to check that the ELK server is running?
Navigate to http://publicIP(elkserver):5601


Specific commands the user will need to run to download the playbook, update the files, etc.


SPECIFIC COMMAND
APPLICATION
ssh-keygen
Create ssh key 
sudo cat .ssh/id_rsa.pub
View ssh public key
ssh azadmin@20.222.104.28
ssh azadmin@10.0.0.4
Ssh azadmin@10.1.0.7
Ssh azadmin@10.1.0.8
Access to jump box via ssh
Access ro ELK VM
Access to VM2
Access to VM3
sudo docker container list -a
Displays all containers
sudo docker start wonderful_lovelace
 start wonderful_lovelace container
sudo docker ps -a
List container status
sudo docker attach wonderful_lovelace
attach to wonderful_lovelace container
cd /etc/ansible
Change ansible directory
ls -laA
List all hidden and standard files
nano /etc/ansible/hosts
Edit hosts file
nano /etc/ansible/ansible.cfg
Edit ansible.cfg file
nano /my_playbook.yml
Edit my_playbook
ansible-playbook install_elk_playbook.yml
Install playbook
Ansible-playbook [location filename]
Run ansible playbook
Cd /etc/ansible/roles
Change into roles directory
ansible-playbook install_filebeat.playbook.yml
 Install filebeat to playbook
ansible-playbook install_metricbeat.playbook.yml
 Install metricbeat to playbook
sudo apt-get update
Update all packages
sudo systemctl status docker
sudo systemctl start docker
sudo docker pull cybersecurity/ansible
sudo docker run -ti cybersecurity/ansible bash
ansible -m ping all
curl -L -O [file location]
dpkg -i [filename]
http://20.214.0.4:5601//app/kibana 
Docker status
Docker start
Docker container file pull
Docker container image, run and create
Ansible containers, connection check
File download from web location
File install [filebeet, metricbeat]
Access Kibana from web browser





