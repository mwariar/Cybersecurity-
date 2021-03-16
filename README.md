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

