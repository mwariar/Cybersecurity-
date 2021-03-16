
#Day 1: ELK Installation

##Part 1: Creating a New vNet

- Created New vNet called RedTeamNetwork_ELK

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/VNet_ELK.PNG)
 
- Creating Peer connection between the 2 vNets in different locations

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/Peer_connection.PNG) 
 
##Part 2: Creating a New VM

- New VM Web-4 created with IP 10.1.0.4 (Pub IP 20.51.230.217)	 

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/VM_ELK.PNG) 

- Verify that it works as expected by connecting via SSH from the Ansible container to the VM Web-4

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/SSH.PNG)  

##Part 3: Downloading and Configuring the Container

- Adding elk group in Hosts file
 
	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/Host_ELK.PNG) 

- ELK Container Download 
 
	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/ELK_playbook.PNG) 


##Part 4: Launching and Exposing the Container
 
	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/Launch_playbook.PNG) 
	
	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/Launch_playbook2.PNG) 

- SSH to Web-4 VM and check if docker image and container are running

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/Docker_ps.PNG) 
 
##Part 5: Identity and Access Management

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/Security_rules.PNG) 

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/Kibana_check.PNG) 
  
#Day 2: Filebeat Installation

- Creating Playbook to include all the steps for Filebeat installation

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/Filebeat_install.PNG) 

##Part 1: Installing Filebeat on the DVWA Container

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/Filebeat_config.PNG) 

##Part 2: Creating the Filebeat Configuration File

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/ELK_playbook.PNG) 
 

- The IP address of the ELK VM is updated in the filebeat-config.yml file and then copied to the remote VM.

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/ELK_configupdate.PNG) 

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/ELK_configupdate2.PNG) 

	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/copy_config.PNG) 
 
##Part 3: Creating the Filebeat Installation Play

	 ![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/filebeat_playbook.PNG) 

- Deploying the playbook on web servers.
 
	![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/filebeat_success.PNG) 

##Part 4: Verifying Installation and Playbook

- Data pull to Kibana tested 

	 ![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/data_pull.PNG) 

	 ![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/kibana_fb.PNG) 
##Bonus: Creating a Play to Install Metricbeat

**Same process followed for Metric beat.**

- YML File

	 ![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/YML_file.PNG) 

- Execution Success

	 ![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/SB_Execution.PNG) 

- Checking Kibana for data upload

	 ![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/data_pullsuccess.PNG) 

	 ![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Activities/kibana_sb.PNG) 
 
