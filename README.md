## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/102446133/160266681-23946cc1-ebe2-4de5-acef-d5143ef2dea3.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Elk Deployment file may be used to install only certain pieces of it, such as Filebeat.

  - [myfirstplaybook.yml](https://github.com/kattleyas/cautious-couscous/blob/9c84bd7f54609b17aa9f84db7f06bf6c6840e0ee/myfirstplaybook.yml)
  - [Hosts](https://github.com/kattleyas/cautious-couscous/blob/fb6ddbd032367b2ee37b7fead09132cafc2ed186/Hosts)
  - [ansible.cfg](https://github.com/kattleyas/cautious-couscous/blob/cd0056fc9c9b0b42e2965d25fb62ac7d9a531c82/ansible.cfg)
  - [install-elk.yml](https://github.com/kattleyas/cautious-couscous/blob/7e6c4bad977d56066a47a2db83b73cfca11ecdf5/install-elk.yml)
  - [filebeat-config.yml](https://github.com/kattleyas/cautious-couscous/blob/c1b57909397aab20b46ce5f9ad71de9294427a8c/filebeat-config.yml)
  - [filebeat-playbook.yml](https://github.com/kattleyas/cautious-couscous/blob/4a14cf73f89705ffffd03587ddf5e3fe0debb95c/filebeat-playbook.yml)
  - [Metricbeat-Config.yml](https://github.com/kattleyas/cautious-couscous/blob/13a020f7d521e7ea28688af401d8d4db354c07d3/Metricbeat-Config.yml)
  - [Metricbeat-Playbook.yml](https://github.com/kattleyas/cautious-couscous/blob/fdcc0014db63c4719528407134ba80da919c6f64/Metricbeat-Playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly functional and available, in addition to restricting traffic to the network.

  - What aspect of security do load balancers protect?
    - Load balancers reroute live traffic from one server to another
    
- What is the advantage of a jump box?
    - Prevents Azure VMs exposed via a public IP. 
    - IP addresses that can communicate with the Jump Box and also be restricted.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.

- What does Filebeat watch for?
  - Filebeat monitors log files, collects log events, and forwards them to Elasticsearch or Logstash for indexing.
  
- What does Metricbeat record?
  - Collects metrics and statistics ans ships them to the output specified.

The configuration details of each machine may be found below.

| Name       | Function | IP Address    | Operating System     |
|------------|----------|---------------|----------------------|
| Jump Box   | Gateway  | 138.91.175.73 | Linux (ubuntu 18.04) |
| Web-1      | DVWA     | 10.0.0.5      | Linux (ubuntu 20.04) |
| Web-2      | DVWA     | 10.0.0.6      | Linux (ubuntu 20.04) |
| Elk-Server | ELK      | 10.1.0.4      | Linux (ubuntu 20.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My public IP through TCP 5601

Machines within the network can only be accessed by Workstation and Jump-Box-Provisioner through ssh Jump-Box.

- Which machine did you allow to access your ELK VM?
  - Jump-Box-Provisioner IP 138.91.175.73

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | IP AddressAllowed IP Addresses |
|------------|---------------------|--------------------------------|
| Jump Box   | Yes                 | Personal IP                    |
| Web-1      | No                  | 138.91.175.73                  |
| Web-2      | No                  | 138.91.175.73                  |
| Elk-Server | No                  | 138.91.175.73 & Personal IP    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
  
- What is the main advantage of automating configuration with Ansible?
  - Playbook can be used to scale automation on multiple machines
  - No custom code is necessary to automate systems

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc.

- User More Memory   
    ![Use more memory](https://user-images.githubusercontent.com/102446133/160270636-f69825c4-1f63-48d9-8117-7222b565ca39.png)

- Install docker.io 

    ![Install Docker.io](https://user-images.githubusercontent.com/102446133/160270826-4791f9e3-e785-4d23-8721-46e88472066a.png)
    
- Install python3-pip

    ![Install python3-pip](https://user-images.githubusercontent.com/102446133/160270953-409011fc-bded-4a06-a03a-149b3d345125.png)
    
- Install Docker module

    ![Install Docker module](https://user-images.githubusercontent.com/102446133/160271072-6ee32cf0-589c-49b6-86cb-d91462d057ab.png)
    
- Increase Virtual Memory

    ![Increase virtual memory](https://user-images.githubusercontent.com/102446133/160271132-cc3ba505-4aaf-4d5a-9ce5-747910092d1e.png)
    
- Download and Launch a docker Elk container

    ![Download and Launch a docker Elk](https://user-images.githubusercontent.com/102446133/160271192-919bcab3-e3d7-4987-be51-46019be8a213.png)
    
- Enable service docker on boot

    ![Enable docker on boot](https://user-images.githubusercontent.com/102446133/160271231-70256215-ebe1-4b5d-aaec-2ed1fd3b3780.png)


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ElkServer](https://user-images.githubusercontent.com/102446133/160271798-7179ec34-6998-4699-8d0b-597ae478dc4a.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is used to collect log files used by analysts to monitor for suspicious activity
- Metricbeat collects more specific metrics such as CPU usage and uptime

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yml file to ansible folber.
- Update the config file to include users and ports.
- Run the playbook, and navigate to Kibana http://[your.BM.IP]:5601/app/kibana to check that the installation worked as expected.

### For ELK VM COnfiguration
- Copy the [install-elk.yml](https://github.com/kattleyas/cautious-couscous/blob/7e6c4bad977d56066a47a2db83b73cfca11ecdf5/install-elk.yml)
- Run the playbook using this command: ansible-playbook /etc/ansible/install-elk.yml




### Commands the user will need to run and download the playbook, update the files, etc._# Elk-Stack-Project
Elk-Stack-Project
- SSH into JumpBox by running ssh RedAdmin@[publicip]
- Run sudo docker start [ansible container name]
- Run sudo docker attach [ansible container name]
- Update hosts file in /etc/ansible/hosts
- Create new ansible playbook for the Elk VM by running curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/filebeat-config.yml
- Run anible-playbook install-elk.yml
- Check elk-docker container is running by running ssh RedAdmin@[Elk private IP]
- Run sudo docker ps


