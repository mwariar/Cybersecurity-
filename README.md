## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Network_Diagram.PNG)


[ELK Playbook File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/playbook2_elk.yml) has been tested and used to generate a live ELK deployment on Azure. 

Following Files can be used only to install only certain pieces of it, such as Filebeat, Metricbeat etc which helps to send log of specific details required to LogStash.

[FileBeat Playbook File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/filebeats_play.yml)
[Metric Playbook File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/metricsbeats_play.yml)

Below mentioned configration Files are used for confuring IP addresses of VM machine w/ELK stack docker.
[Playbeat Configration File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/playbeats_config.yml)
[Metric Configration File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/metricbeats_config.yml)


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient by distributing the tasks over a set of resources (VMs) and avoiding uneven overload. It also retricts access to to the Virtual cloud network and helps in monitoring and preventing DDoS attacks.

Network Security is a major factor in cloud computing and needs to be monitors at all times. The best way to secure the network is to minimize the exposure to external Cloud Network. Jump Box and Load Balancers play a major role in minimizing the exposure to external environment.

#### JumpBox and Its Advantages
- Jumpbox acts as a intermediary host or an SSH gateway to a remote network and can be used to access and manage devices in separte security zone
- Jumpbox is given public IP address which is used to enable connectivity of on-premise network to Azure's virtual network over the internet
- By using the network security group, we can restrict the external IP addresses to communicate with the Jump box. It helps to improve security and we can do monitoring and logging on a single box.
- In our project, we have used installed Docker and Ansible on our jumpbox and used YML scripts to configure our Web servers with different applications and stacks
	- Deployed Docker and DVBA containers to our web servers to provide pentesting application to the red team testers
	- Deployed Filebeat and MetricBeat applications to specifically extract the syslogs and docker logs from the web server and pass it on to Logstash at 5044 server
	- Deployed Docker and ELK Stack containers to one of the VM which monitors the auth+syslogs and docker logs
- We did all these deployement with just 3 scripts and we can add n number of IPs to be updated in the host file of the ansible

#### Security Aspect of Load Balancers
- Load Balancers Distribute network traffic across multiple servers, thus 
	- Ensuring no single server is overloaded
	- Improved application responsiveness
- Manage the flow of information between an endpoint device and the virtual server 
- Conduct continous health check on virtual servers to ensure they can handle requests and if necessary, removes unhealthy servers from the pool until they are restored
- Defends an organization against distributed denial-of-service (DDoS) attacks by shifting attack traffic from the corporate server to a public cloud provider
- In terms of OSI model, load balancing happens between layers four to seven (L4-Transport, L5-Session, L6-Presentation and L7-Application).


#### ELK Stack
- Acts as a powerful monitoring tool by 
	- Aggregating logs from all your systems and applications in **LogStash**
	- Analyze these logs by using **ElasticSearch**
	- Create visualizations for application and infrastructure monitoring, faster troubleshooting, security analytics etc. in **Kibana**
- Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the auth and system logs.  
- Auth and system logs have huge amount of data but we might need only specific details to monitor the logs. Beats application helps in extracting only the specific details to be stored in Logstash. Few examples are:
	- FileBeat 
		- Acts as an agent for forwarding and centralizing log data on your servers
		- Monitors the log files or locations that you specify, collects log events, and forwards them either to Logstash for indexing

	- MetricBeat
		- Acts as an agent to periodically collect metrics from the operating system and from services running on the server. 
		- Sends the metrics and statistics that it collects to Elasticsearch

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.
| Name   |  Function                                          | IP Address    |  Public IP   |  Operating System   |
|--------|----------------------------------------------------|---------------|--------------|---------------------|
|JBox    |SSH Gateway and Anisble Docker Container            |10.0.0.4       |13.83.87.195  |Linux                |
|Web-1   |Virtual Server with PVBA Docker Container and Beats |10.0.0.5       |104.42.41.103 |Linux                |
|Web-2   |Virtual Server with PVBA Docker Container and Beats |10.0.0.7       |104.42.41.103 |Linux                |
|Web-3   |Virtual Server with PVBA Docker Container and Beats |10.0.0.6       |104.42.41.103 |Linux                |
|Web-4   |Virtual Server with ELK Stack (Monitoring           |10.1.0.4       |13.83.87.195  |Linux                |


![Virtual Machines](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Virtual_Machines.PNG)

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump box machine **Jbox** can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 142.117.81.26 at Port 22

Machines within the network can only be accessed by JumpBox Ansible Contatainer and Load Balancer.

- ELK VM can be accessed by external cloud (allowed IP Address : 142.117.81.26) on port 5601.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses (Inbound)|
|----------|---------------------|-------------------------------|
| Jump Box | Yes                 | 142.117.81.26                 |
| Web-1    | No (through LB)     | 10.0.0.4                      |
| Web-2    | No (through LB)     | 10.0.0.4                      |
| Web-3    | No (through LB)     | 10.0.0.4                      |
| Web-4    | Yes                 | 142.117.81.26                 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because:
- the feasibility of human errors reduced drastically 
- the ease of provisioning and maintaining various VM/web servers 
- Configration Management - 
	- Change the configuration of an application, OS, or device; 
	- Start and stop services
	- Install or update applications
	- Implement a security policy; 
	- Perform a wide variety of other configuration tasks.
- Deploying in n number of VMs by mantaining a single Host File

The playbook implements the following tasks:

````
- Install **Docker.io** 
- Install Python by running **apt install python3-pip**
- Install Pip Docker Python Module
- Increase the virtual Memory by running sysctl ansible module and increase the **vm.max_map_count = 262144**
- Install the ELK Stack by pulling **sebp/elk:761** container image from hub.docker.com and opening the respective ports (5601, 9200, 5044)
- Enable the Docker Services on Startup

````

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Docker_PS_Image.PNG)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

| Name   | IP Address    |
|--------|---------------|
|Web-1   |10.0.0.5       |
|Web-2   |10.0.0.7       |
|Web-3   |10.0.0.6       |

We have installed the following Beats on these machines:
-** FileBeat **
	- Acts as an agent for forwarding and centralizing log data on your servers
	- Monitors the log files or locations that you specify, collects log events, and forwards them either to Logstash for indexing

-** MetricBeat**
	- Acts as an agent to periodically collect metrics from the operating system and from services running on the server. 
	- Sends the metrics and statistics that it collects to Elasticsearch


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

The steps to configure ELK stack has been mentioned ablove. 

SSH into the control node and follow the steps below to configure Beats into target machines:

- Download the installation file for Filebeat by running below command
	'curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.8.1-amd64.deb'
- Install the Filebeat Package by running below command
	'dpkg -i filebeat-oss-7.8.1-amd64.deb'
- Download the filebeat congfigration file to the container
	`curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/filebeat-config.yml'
- Update the host field with your ELK-VM's IP address. Copy this configration file from ansible container to target machine so that the logs are correctly shipped to Logstash and KibanaYou can use the copy ansible module
````	
	copy:
          src: /etc/ansible/filebeat-config.yml 
          dest: /etc/filebeat/filebeat.yml

````
- Enable the filebeat modules 'filebeat modules enable system'
- Setup the filebeat 'filebeat setup' 
- Start the filebeat service 'service filebeat start' 
- Enable the filebeat service on boot

````	
    systemd:
      name: filebeat
      enabled: yes
````
- Update the `**/etc/ansible/hosts**` file with specific blocks and IP address and refer to that block in hosts tab in playbook
- Compile the [FileBeat Playbook File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/filebeats_play.yml)
- Check whether the ansible in able to target the target machines by running the below code:
	`**ansible all -m ping**`
- If the ping is successful, we can deploy the Beats to the VM by running below command:
	`**anisble-playbook filebeats_play.yml**`
- To check whether the log data is getting shipped to Logstash, we can visit the [Kibana website](http://20.51.230.217:5601/app/kibana#/home)
