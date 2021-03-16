## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://github.com/mwariar/Cybersecurity-/blob/main/Images/Network_Diagram.PNG)


[ELK Playbook File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/playbook2_elk.yml) has been tested and used to generate a live ELK deployment on Azure. 

Following Files can be used only to install only certain pieces of it, such as Filebeat, Metricbeat etc which helps to send log of specific details required to LogStash.

[FileBeat Playbook File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/filebeats_play.yml)
[MetricBeat Playbook File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/metricsbeats_play.yml)

Below mentioned configration Files are used for confuring IP addresses of VM machine w/ELK stack docker.
[Playbeat Configration File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/playbeats_config.yml)
[MetricBeat Configration File](https://github.com/mwariar/Cybersecurity-/blob/main/Ansible/metricbeats_config.yml)
