## ALEXANDER PEACE

# cybersecurity_projects
Repository For CyberSecurity School
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/50026505/94481447-f14bdb00-0194-11eb-9e22-791b47448d3d.png)



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.
- [Setup Webserver Operating System](Ansible/Pentesting.yml.txt)
- [Configure Filebeat hosts](Filebeat/Filebeat_Configure_Installation.yml.txt)
- [Install FileBeat](Filebeat/Setup_Filebeat.yml.txt)
- [Configure Hosts to Run Ansible](Ansible/HOSTS_File.yml.txt)
- [Install Elk Container](Elk/ELK_Configure_Installation.yml.txt)
  

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to increasing access to the network.
Load Balancing prevents DDoS (Denial of Service) Attacks, by switching traffic from the attacked server to a different sever. 
A Jumpbox Server protects our system by securing VLANS using a firewall. It also has the ability to update and create/recreate operating systems for our Network with ease. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system operating system.
- Filebeat will monitor logs that have been recorded in the servers.
- Metricbeat will monitor metrics and measure statistics from the server periodically and output them into a report. 

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  |40.125.67.5 | Linux            |
| Web-01   | Network  | 10.0.0.9   | Linux            |
| Web-02   | Network  | 10.0.0.12  | Linux            |
| Web-03   | Network  | 10.0.0.13  | Linux            |

### Access Policies

The VMs on the internal network are not accessable from the public internet.
Only the Jumpbox VM accepts connections from the internet and only from specified IPs.
The Current configuration for set for the jumpbox to only accept the users home IP address.
Machines in the network are accessed only through the jumpbox.
A screeshot of the access policies are linked here:

![Images_FirwallRuleScreenshot](https://user-images.githubusercontent.com/50026505/94484794-3a525e00-019a-11eb-9c45-04aa91de2cef.JPG)

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 67.186.247.232

Machines within the network can only be accessed by JumpBoxProvisioner.
- JumpBoxProvisioner AzureUser@40.125.67.54

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JumpBox  | No                  | 10.0.0.9 10.0.0.12   |
                                                     
                                                     

### Elk Configuration
(ELK/ELK_Configure_Installation.yml.txt)
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- You can set up the Elk Container without being inside the Elk Stack. 
- It makes management of the Elk Stack Operating System easier (Easier to update remotely). 
- It also allows us to maximize storage for intallation
- Allows users to install partial packages.
- Reduces the recovery time for the Elk Server 
- Increases ability to create a duplicate

The playbook implements the following tasks:
- Install Docker so that containers can be configured in the Elk Server
- Install Python3 and and install docker within python3
- Increase virtaul memory automatically when Elk is booted
- Download and Launch a docker container for Elk
- Enable the docker container created

![image](https://user-images.githubusercontent.com/50026505/94483863-c6638600-0198-11eb-9b27-5df24d7551d5.png)

The Second image is part of the first:

![image](https://user-images.githubusercontent.com/50026505/94483883-cfecee00-0198-11eb-8a75-8960d23302eb.png)


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/50026505/94483939-e430eb00-0198-11eb-8da9-a58c1b0ac667.png)

![image](https://user-images.githubusercontent.com/50026505/94483953-e98e3580-0198-11eb-9138-f4fdf725447e.png)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:
- Web-01 10.0.0.9
- Web-02 10.0.0.12
- Web-03 10.0.0.13

We have installed the following Beats on these machines:
- Filebeat 
- Winlogbeat
- Metricbeat
- Auditbeat

These Beats allow us to collect the following information from each machine:
- These beats allow administrators to monitor the seperate operating systems in the network. It also is useful in monitoring security and unusual activity. 
- Winlogbeat will develop a report based on Windows event logs.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible.
- Update the filebeat-confiig.yml file to include the IP Address of the Elk Virtual Machine
- Run the playbook, and navigate to http://10.2.0.4:5601/app/kibana to check that the installation worked as expected.

To setup Filebeat:
- Nano /etc/filebeat/filebeat-configuration.yml
- Scroll to output.elasticsearch: and adjust the hosts line to the elk server's IP Address
- Scroll to setup.kibana: and adjust the hosts line to the elk server's IP Address:5601
- Exit and save the configuration file
- Create a new .yml file (example FilebeatInstall.yml)
- After the filebeat playbook is played run ansible-playbook 'name-of-your-file.yml'


THE END

## END ##
