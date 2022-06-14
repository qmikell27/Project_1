# Project_1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

~/OneDrive/Desktop/QM_HW_Projects/Project_1/Diagrams/elkdiagramss.PNG

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Congig and Yaml files may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
<<<<<<< HEAD
ansible.cfg       
filebeat-config.yml   
hosts          
metricbeat-config.yml
dockerinstall.yml 
filebeat-playbook.yml  
installelk.yml 
metricbeat-playbook.yml
=======
>>>>>>> 229f1fa686aa0c6c82f2992dc99a98b60f08bbc6


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly dependable, in addition to restricting traffic to the network.
- _TODO: What aspect of security do load balancers protect? 
The load balancers protect the systems from various attacks, especially DDoS attacks which sole aim is to overload the servers. The load balancers ensure that the activity hitting the sites is spread between the servers so as to not overload a single server. This balancing ensures that the websites will be available which is an important aspect of their deployment
What is the advantage of a jump box?
The advantage of using a jump box is to allow access into the server by using a single node which is monitored and used by a single user. There is only one way into jump box which is secured by using encrypted public and private keys which only exist on the user’s machine. This one way in, one way out access adds an additional level of security and transparency for the administrator

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- _TODO: What does Filebeat watch for?_
Filebeat is a lightweight shipper for forwarding and centralizing log data. This means that Filebeat monitors the information in a file system and it logs the file and any changes made to the file if it notices any changes it will report on what was changed and when. Essentially Filebeat is a watchdog for file/locations and logs and keeps track of these events
- _TODO: What does Metricbeat record?_
Metricbeat is a lightweight shipper which can be installed on servers to collect metrics from the operating system, and from services running on the server. This means that Metricbeat collects data on a server and sends them to an output that the user specifies. The user can then analyze the data and statistics gathered by Metricbeat to make important decisions about the servers

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

|   Name  |  Function  | IP Address |       O.S.       |
|:-------:|:----------:|:----------:|:----------------:|
| JumpBox |   Gateway  |  10.0.0.4  |       Linux      |
|  Web-1  |   Server   |  10.0.0.5  |       Linux      |
|  Web-2  |   Server   |  10.0.0.6  |       Linux      |
|  Elk VM | Elk Server |  10.1.0.4  |       Linux      |




### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumbBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_
The whitelisted IP address to gain access to the JumpBox: Admin (My Personal IP)

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
The only machine that has access to the ELK VM has the private IP address 10.0.0.4 via SSH Port 22

A summary of the access policies in place can be found in the table below.

|   Name  | Publicly Accessible | Allowed IP Address | Operating System |
|:-------:|:-------------------:|:------------------:|:----------------:|
| JumpBox |          Yes        |      Admin IP      |       Linux      |
|  Web-1  |          NO         |      10.0.0.5      |       Linux      |
|  Web-2  |          NO         |      10.0.0.6      |       Linux      |
|  Elk VM |          NO         |      Admin IP      |       Linux      |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
Automating configuration with Ansible allows you to be able to deploy multiple servers using the same playbook file. 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
•	Install Docker.io
•	Install Python-pip
•	Install Docker Container
•	Download Launch Docker Container: Elk
•	Enable Docker Service on Boot


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
~/OneDrive/Desktop/QM_HW_Projects/Project_1/Diagrams/dockerps.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
Web-1 (10.0.0.5) and Web-2 (10.0.0.6)
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
Filebeat - Metricbeat
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- Filebeat monitors log files or locations and collects log events. The events are then sent to Elasticsearch or Logstash for later use. In these logs we are able to see system logs and any changes or activity within the files. 
-Metricbeat collects the metrics from the operating system and from anything running on the server. We can see things such as the time and location of user accessing the server as well as the type of operating system and even the referrer to the server
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
/etc/ansible/filebeat-playbook.yml /etc/ansible/filebeat-config.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?
http://20.122.85.68:5601/app/kibana
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

