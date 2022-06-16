# Project_1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
<img width="480" alt="elkdiagramss" src="https://user-images.githubusercontent.com/107008734/173701468-ae5a65e4-0402-4439-ae1f-bf7587e65d2f.PNG">


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Configuration and Yaml files may be used to install only certain pieces of it, such as Filebeat.

- [Install Elk](https://github.com/qmikell27/Project_1/blob/main/Ansible/installelk.yml)
- [Docker Vm Install](https://github.com/qmikell27/Project_1/blob/main/Ansible/dockerinstall.yml)
- [Filebeat Config](https://github.com/qmikell27/Project_1/blob/main/Ansible/filebeat-config.yml)
- [Filebeat Playbook](https://github.com/qmikell27/Project_1/blob/main/Ansible/filebeat-playbook.yml)
- [Hosts](https://github.com/qmikell27/Project_1/blob/main/Ansible/hosts)
- [Metricbeat Config](https://github.com/qmikell27/Project_1/blob/main/Ansible/metricbeat-config.yml)
- [Metricbeat Playbook](https://github.com/qmikell27/Project_1/blob/main/Ansible/metricbeat-playbook.yml)
- [Ansible Config](https://github.com/qmikell27/Project_1/blob/main/Ansible/ansible.cfg)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly dependable, in addition to restricting traffic to the network.
What aspect of security do load balancers protect? 
The load balancers protect the systems from various attacks, especially DDoS attacks which sole aim is to overload the servers. The load balancers ensure that the activity hitting the sites is spread between the servers so as to not overload a single server. This balancing ensures that the websites will be available which is an important aspect of their deployment.
What is the advantage of a jump box?
The advantage of using a jump box is to allow access into the server by using a single node which is monitored and used by a single user. There is only one way into jump box which is secured by using encrypted public and private keys which only exist on the user’s machine. This one way in, one way out access adds an additional level of security and transparency for the administrator.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

Filebeat is a lightweight shipper for forwarding and centralizing log data. This means that Filebeat monitors the information in a file system and it logs the file and any changes made to the file if it notices any changes it will report on what was changed and when. Essentially Filebeat is a watchdog for file/locations and logs and keeps track of these events

Metricbeat is a lightweight shipper which can be installed on servers to collect metrics from the operating system, and from services running on the server. This means that Metricbeat collects data on a server and sends them to an output that the user specifies. The user can then analyze the data and statistics gathered by Metricbeat to make important decisions about the servers

The configuration details of each machine may be found below.


|   Name  |  Function  | IP Address |       O.S.       |
|:-------:|:----------:|:----------:|:----------------:|
| JumpBox |   Gateway  |  10.0.0.4  |       Linux      |
|  Web-1  |   Server   |  10.0.0.5  |       Linux      |
|  Web-2  |   Server   |  10.0.0.6  |       Linux      |
|  Elk VM | Elk Server |  10.1.0.4  |       Linux      |




### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumbBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

The whitelisted IP address to gain access to the JumpBox: Admin (My Personal IP)

Machines within the network can only be accessed by _____.
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

Automating configuration with Ansible allows you to be able to deploy multiple servers using the same playbook file. 


### Elk Server Set Up Instructions

- Create New Virtual Net
- Create Peering Rules
- Create Elk Server VM
- Create Ansible Playbook
- Download Configuration To Container
- Launch Container

       
     1.Create New Virtual Network 
       * Enter The Previous Resource Group You Have Been Using And Create A New VNet
       * Make Sure They Are Included In The Same Region
Elk VNet
<img width="567" alt="CreateElkVnet" src="https://user-images.githubusercontent.com/107008734/173940813-af7a127f-195f-4fd8-9b44-7cf6b34a7cb2.PNG">
Elk Vnet Subnets 
<img width="1199" alt="elksubnets" src="https://user-images.githubusercontent.com/107008734/173941883-7b9815cd-0d35-4f48-aa79-6c25b44ac871.PNG">
Elk SecRule
<img width="306" alt="elk security rules2" src="https://user-images.githubusercontent.com/107008734/173976082-1fce1c6d-07cc-4aa0-bedb-12017e25bb3e.PNG">
<img width="604" alt="ServerSecRule2" src="https://user-images.githubusercontent.com/107008734/173975889-48fc2df0-4dbf-4df5-a038-031a7c175d53.PNG">
    2. Create Two Pronged Peering Rule
       * Elk To Red And Red To Elk
<img width="1122" alt="Peerings" src="https://user-images.githubusercontent.com/107008734/173940920-7873cad6-4a09-4d41-8b3d-22a38c4a7f6b.PNG">
<img width="991" alt="peerings2" src="https://user-images.githubusercontent.com/107008734/173940986-797ae146-03d2-48f4-b322-3135ccf460a5.PNG">

    3. Create The Elk Server VM 
       * Make Sure The IP Public Ip Address Matches Your Local Machine In The Security Settings
       * Make Sure Your Elk VM Is In The Same Region As Your Virtual Net
       * Once The VM Is Created And Deployed You Must SSH Into The Jump Box
       * Once Into Your Jump Box Its Time To Created A Public/Private Key Paring Use The Command SSH-Keygen
       * Once Completed Cat The Public Key Using The Command cat /.ssh/id_rsa.pub
       * Copy The Pub Key And Navigate To YOur Elk Server On Azure And Paste The Public Key Into The Password Reset Menu
Elk VM
<img width="687" alt="createElkVM" src="https://user-images.githubusercontent.com/107008734/173940504-1660b43a-fdca-45c3-87de-cdc5339c30cb.PNG">
<img width="1141" alt="ElkVm2" src="https://user-images.githubusercontent.com/107008734/173942538-c1783a25-ad07-4e6b-8af7-ab4e7c29b15e.PNG">
    4. Create Ansible Playbook
       * Using A Template Or Your Text Editor Of Choice Create An Ansible Playbook For The Configuration And File Download
        
        Install Elk File
<img width="531" alt="installelkyml" src="https://user-images.githubusercontent.com/107008734/173979580-4b56fb10-273a-49be-8994-513d621e8200.PNG">
        Edit /etc/ansible/hosts
<img width="540" alt="nanoansiblehosts" src="https://user-images.githubusercontent.com/107008734/173980299-dfe553a1-9a7c-4291-b399-12103e296c18.PNG">
    5. Download The Configuration To The Container
    6. Launch The Container
     

The playbook implements the following tasks:
•	Install Docker.io
•	Install Python-pip
•	Install Docker Container
•	Download Launch Docker Container: Elk
•	Enable Docker Service on Boot

SSH Into Elk@ElkPrivateIP

<img width="396" alt="sshinto elkvm" src="https://user-images.githubusercontent.com/107008734/173981078-1b2fc210-3bd8-41fa-8133-f7474ff689e7.PNG">

Check The Status Of Docker
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="616" alt="dockerpselk" src="https://user-images.githubusercontent.com/107008734/173719696-30f6a0d7-4cb1-4d47-8463-079a4493e685.PNG">


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 (10.0.0.5) and Web-2 (10.0.0.6)
We have installed the following Beats on these machines:
Filebeat - Metricbeat
These Beats allow us to collect the following information from each machine:
- Filebeat monitors log files or locations and collects log events. The events are then sent to Elasticsearch or Logstash for later use. In these logs we are able to see system logs and any changes or activity within the files. 
- Metricbeat collects the metrics from the operating system and from anything running on the server. We can see things such as the time and location of user accessing the server as well as the type of operating system and even the referrer to the server
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the - [Install Elk](https://github.com/qmikell27/Project_1/blob/main/Ansible/installelk.yml),- [Filebeat Config](https://github.com/qmikell27/Project_1/blob/main/Ansible/filebeat-config.yml)- [Metricbeat Config](https://github.com/qmikell27/Project_1/blob/main/Ansible/metricbeat-config.yml) file to Ansible container folder.
- Copy the - [Filebeat Playbook](https://github.com/qmikell27/Project_1/blob/main/Ansible/filebeat-playbook.yml) and - [Metricbeat Playbook](https://github.com/qmikell27/Project_1/blob/main/Ansible/metricbeat-playbook.yml) to the Ansible container folder 
- Update the /etc/ansible/host file to include Elk Server IP 10.1.0.4
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it?_
ansible-playbook filebeat-playbook.yml ansible-playbook metricbeat-playbook.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
Navigate to /etc/ansible/host edit the file to add webserver/elkserver ip address.  
- _Which URL do you navigate to in order to check that the ELK server is running?
http://[ELK-VM.Public IP]:5601/app/kibana
<img width="224" alt="kibana ip" src="https://user-images.githubusercontent.com/107008734/173982186-a2859f62-aafb-48c7-bcf2-54f14eeec5be.PNG">

If Done Correctly You Should See The Following Kibana Page

<img width="1051" alt="kibana home page" src="https://user-images.githubusercontent.com/107008734/173981945-444e2c3f-91ce-4a2f-9b15-bcf7696e89b7.PNG">

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

|                         Command                         |                          Description                          |
|:-------------------------------------------------------:|:-------------------------------------------------------------:|
|               ssh [user name]@[Jumpbox IP               |                      Connects to JumpBox                      |
|                        ssh-keygen                       |               Generates Public/Private Key Pair               |
|                  cat ~./ssh_/id_rsa.pub                 |                  Cats Public Key To Terminal                  |
|              sudo docker container list -a              |              Lists The Containers On The Machine              |
|            sudo docker start [container name]           |                   Starts The Named Container                  |
|           sudo docker attach [container name]           |                  Attaches The Named Container                 |
|                           Exit                          |     Exits The Container (Exit A Second Time Exits Ansible)    |
|                     cd /etc/ansible                     |               Changes Directory To /Etc/Ansible               |
|                nano /etc/ansible/(hosts)                |               Opens Ansible (Hosts) File To Edit              |
|              nano /etc/ansible/ansible.cfg              |               Opens Ansible Config File To Edit               |
|   nano filebeat-config.yml nano filebeat-playbook.yml   |  Opens Filebeat File To Edit Opens Filebeat Playbook To Edit  |
| nano metricbeat-config.yml nano metricbeat-playbook.yml | Opens Metricbeat File To Edit Opens Filebeat Playbook To Edit |
|             ansible-playbook [filename.yml]             |                     Executes The Playbook                     |
|                                                         |                                                               |
