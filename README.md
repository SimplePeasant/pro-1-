CyberSecurity_BootCamp_Project_1

The files in this repository were used to configure the network depicted below.

(https://github.com/SimplePeasant/pro-1-/blob/main/Diagram/Project%231.drawio.pdf)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Project 1 Red Team Network Diagram file may be used to install only certain pieces of it, such as Filebeat.

filebeat-playbook.yml
filebeat-config.yml
metricbeat-playbook.yml
metricbeat-config.yml
elk-playbook.yml

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly operational in addition to restricting high-traffic to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
- Load Balancing plays an important security role as computing moves evermore to the cloud. The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider.

• It helps prevent overloading servers as well as optimizes productivity and maximizes uptime.
• It also creates resiliency allowing rerouting live traffic from one server to another causing it to eliminate single points of failure from attacks such as DDoS attack.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the  network and system logs.
- _TODO: What does Filebeat watch for?_

It monitors the log files/locations that you specify and forwards them to Elasticsearch/Logstash for indexing.

- _TODO: What does Metricbeat record?_

It records metrics/statistics data and transports them to the output that you specifics thru Elasticsearch/Logstash.



The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    |  server  | 10.0.0.4   | Linux            |
| Web-2    |  server  | 10.0.0.6   | Linux            |
|Web-3(elk)|  server  | 10.2.0.4   | Linux                 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump-box-provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 20.42.58.10 Local Host IP Address

Machines within the network can only be accessed by Jump-Box-Provisioner.
- _TODO: Which machine did you allow to access your ELK VM?  
Jump-Box-Provisoner

- What was its IP address?_
Jump-Box (10.0.0.5) 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |    Yes              | 10.0.0.5   |
| web 1    |    no               | 10.0.0.4   |
| web-2    |    no               | 10.0.0.6   |
|web-3(ELK)|    no               | 10.2.0.4   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

One main advantage would be YAML Playbooks. It is the best alternative for configuration management/automation.
It is also able to automate complex multi-tier IT application environemtns

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

SSH into the Jump-Box-Provisioner ssh dijo@20.42.58.10

Start/Attached to the ansible docker (sudo docker start romantic_kilby)/(sudo docker attach romantic_kilby)

then /etc/ansible/ directory and created the ELK playbook (elk_Playbook.yml) 

Run elk_Playbook.yml in same directory (ansible-playbook elk_Playbook.yml) 

then SSH into the Elk-vm to verify the server is up & running.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
https://github.com/SimplePeasant/pro-1-/blob/main/ScreenShots/Web-29ELK%20vm).png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

web 1 ( 10.0.0.4)  web 2 ( 1

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

Filebeat Modules Status &  Metricbeat Modules Status

These Beats allow us to collect the following information from each machine:

- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Filebeat is utilized to gather log files from certin files on remote machines.

Examples would be files that are generated from Microsoft Azure tools, MySQl databases,apache. 


Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server.
Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash..Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash. 



### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

fileB

- Copy the filebeat-configuration.yml file to /etc/ansible/files.
- Update the filebeat-configuration.yml file to include the ELK private IP 10.2.0.4
- Run the playbook-navigate to http:// My.Elk.VM.PublicIP :5601/app/kibana (ELK-VM public IP) Click Add Log Data, Clicked System Logs, Clicked on the DEB tab under Getting Started and then clciked "Check Data" in step 5 to check that the installation was sucsessful.

MetB

- Copy the metricbeat-configuration.yml file to /etc/ansible/roles/files.
- Update the metricbeat-configuration.yml file to include the ELK private IP 10.2.0.4
- Run the playbook-navigate to http://[My.Elk.VM.PublicIP] :5601/app/kibana (ELK-VM public IP) Clicked Add Metric Data - Clicked Docker Metrics - Clicked on the Deb tab - then clciked "Check Data" to confirm that the installation was sucseccful.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook?       Where do you copy it?_
- elk-playbook.yml                   /etc/ansible for elk-playbook.yml 
- metricbeat-playbook.yml                        metricbeat-playbook.yml
- filebeat-playbook.yml                         /etc/ansible/roles for filebeat-playbook.yml                    

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

- /etc/ansible/hosts file (IP of the Virtual Machines).

- _Which URL do you navigate to in order to check that the ELK server is running?

(http://40.91.65.27:5601/app/kibana#/home]:5601/app/kibana)

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

