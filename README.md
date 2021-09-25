# Automated-ELK-Stack-Deployment

Network Topology
This repository contains files to show how to setup or configure a network creates a automated cloud load balancer using a live ELK Deployment using AZURE.   The repository can either aid in partial or full cloud deployment through the use of these files and or configuration.  This repository leverages ansible playbook and beats.

Description 
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Dmn Vulnerable Web Application and leverage GIT repository to upload corresponding files. In order to configure a cloud based network, we need to leverage load balancers.  Load balancers are used to increase capacity (concurrent users) and reliability of applications. They improve the overall performance of applications by decreasing the burden on servers associated with managing and maintaining application and network sessions, as well as by performing application-specific tasks. The load balancer provides an externally-accessible IP address that sends traffic to the correct port on your cluster nodes, provided your cluster runs in a supported environment and is configured with the correct cloud load balancer provider package

Tasks include:
•	Create a new vNet in Azure in a different region, within the same resource group.
•	Create a peer-to-peer network connection between your vNets.
•	Create a new VM in the new vNet that has 2vCPUs and a minimum of 4GiB of memory.
•	Add the new VM to Ansible’s hosts file in your provisioner VM.
•	Create an Ansible playbook that installs Docker and configures an ELK container.
•	Run the playbook to launch the container.
•	Restrict access to the ELK VM.
•	Upload all supporting documents through GitHub

.  


## Acknowledgements

 - [Awesome Readme Templates](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
 - [Awesome README](https://github.com/matiassingers/awesome-readme)
 - [How to write a Good readme](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)

  

## Appendix



  
## Badges

![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=azure-devops&logoColor=white)

![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)

![Ansible](https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible&logoColor=white)

![ElasticSearch](https://img.shields.io/badge/-ElasticSearch-005571?style=for-the-badge&logo=elasticsearch)

![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
    

## Deployment

Why Load Balancing and how does security come into play? 

Load balancing is a tool used to more evenly distribute network or application traffic across multiple servers in a server farm. Each load balancer is located between user/client devices and backend servers, receiving and then distributing incoming requests to any available server capable of fulfilling them.2 
The number of level of requests to the load balancers is usually determined by the load balancing algorithm techniques. Note: The more complex load balancing algorithm techniques are used for higher loads to ensure an evenly distribution of requests.

•	Load Balancers helps prevent overloading servers as well as optimizes productivity and maximizes uptime.
•	Support encrypted communication between clients/users and your load balancers.
•	Can configure to accept traffic only from specific clients and must allow inbound traffic from clients on the listener ports and outbound traffic to the client
•	Can configure to accept traffic only from the load balancer and allow inbound traffic from the load balancer on the listener ports and the health check ports.
•	Can configure to securely authenticate users through an identity provider or using corporate identities. 
•	Leverage a jump server, jump host or jump box which is essentially a separate security system used manage network devices. 
•	Capable of re-routing or distributing live traffic from one server to another eliminating a single points of failure from attacks such as DDoS attack.3

Using Jump-box

A jump server, jump host or jump box is a system on a network used to access and manage devices in a separate security zone. A jump server is a hardened and monitored device that spans two dissimilar security zones and provides a controlled means of access between them.4  In other words, a resource to mitigate or prevent potential hackers to penetrate  or infect the system that is critical or provides  additional configuration to improve overall functionality. It is a hardened remote access server, commonly utilizing Microsoft's Remote Desktop Services or Secure Shell (SSH) software. Administrators have the ability to perform all or most of their administrative tasks via a jump box.

Leveraging and Integrating-ELK-STACK Server 

ELK-STACK is an open-source log analytics solution with three software components: Elasticsearch, Logstash, and Kibana. Working together and allows DevOps and SecOps teams to collect, aggregate, analyze, and visualize log data in the cloud, supporting critical functions like application monitoring and security analytics. 

We leverage this server to do the following:
•	Aggregate log data from a variety of sources using Logstash.
•	Transform, process, and enrich log data using Logstash and Elasticsearch.
•	Index and search log data using Elasticsearch.
•	Explore and analyze log data, and produce data visualizations using Kibana

The Integration and configuration of an ELK server allows the users to easily monitor the vulnerable Virtual Managers(VMs) for any and all changes to the network and or system logs.

There were several tools within ELK-STACK that this repository leveraged to assist in the automation of our cloud based load balancer.  

1.	Filebeat organizes and centralizes log data and once installed, acts as a go-between your servers which forwards them either to Elasticsearch or Logstash for indexing logs.
2.	Metricbeat takes the metrics and statistics that it collects and sends the data based on your specifications, such as Elasticsearch/Logstash.

Storing Access Policies

The machines on the internal network are not exposed to the public Internet. The Jump-Box-Provisioner machine can only accept connections from the Internet and the web VMs can only use the Jump-Box-provisioner’s private IP address.

Jump-Box accessibility is only allowed from the following IP addresses:
•	40.80.149.251 (LocalHost IP address)

ELK VM IP Address:

•	Jump-Box-Provisioner
•	10.1.0.5 (Private)

Built-in Policies

•	Allowed Storage Account SKUs (Deny): Determines if a storage account being deployed is within a set of SKU sizes. Its effect is to deny all storage accounts that don't adhere to the set of defined SKU sizes.
•	Allowed Resource Type (Deny): Defines the resource types that you can deploy. Its effect is to deny all resources that aren't part of this defined list.
•	Allowed Locations (Deny): Restricts the available locations for new resources. Its effect is used to enforce your geo-compliance requirements.
•	Allowed Virtual Machine SKUs (Deny): Specifies a set of virtual machine SKUs that you can deploy.
•	Add a tag to resources (Modify): Applies a required tag and its default value if it's not specified by the deploy request.
•	Not allowed resource types (Deny): Prevents a list of resource types from being deployed.6


Automating configuration with Ansible

Ansible automates provisioning, configuration management, deployment and many other IT needs, freeing up the network and DevOps teams for more strategic work. Ansible can be run from the command line without the use of configuration files for simple tasks, such as making sure a service is running, or to trigger updates or reboots. Ansible also has a collection of modules that can be used to manage various systems as well as cloud infrastructure such as Amazon EC2 and openstack.  better fit in a larger or more homogeneous infrastructure.

Access Policy Summary Chart:

|     Name                          |     Function    |     Operating   System    |     IP Address           |
|-----------------------------------|-----------------|---------------------------|--------------------------|
|     Jump-Box   Provisioner        |     Gateway     |     Linux                 |     40.80.149.251        |
|     ELK-VM(Internal   Network)    |                 |     Azure                 |     10.1.0.5(private)    |
|     VM1(Internal Network)         |                 |     Azure                 |     10.1.0.5(private)    |
|     VM2(Internal Network)         |                 |     Azure                 |     10.1.0.5(private)    |

Virtual Machines within the network can only be accessed by Jump-Box-Provisioner

|     Name                          |     Publicly Accessible    |     IP Address           |
|-----------------------------------|----------------------------|--------------------------|
|     Jump-Box   Provisioner        |             Yes            |     40.80.149.251        |
|     ELK-VM(Internal   Network)    |             No             |     10.1.0.5(private)    |
|     VM1(Internal Network)         |             No             |     10.1.0.5(private)    |
|     VM2(Internal Network)         |             No             |     10.1.0.5(private)    |



•	Simple management & configuration
•	Standardization
•	Rapid automation and deployment of components
•	Easy-to-write scripts 
•	Simple implementation by using readable YAML playbooks
•	Playbooks double as documentation of server environments.
•	Provisioning over SSH. Management sever is not needed

The playbook implements the following tasks(see screenshot which displays the result of running command docker ps  to execute the ELK instance)

SSH into the control node and follow the steps below:

•	SSH into the Jump-Box-Provisioner (ssh azureuser@ 40.80.149.251 )
•	Start/Attached to the ansible docker (sudo docker start “Container Name”)/(sudo docker attach “Container Name”)

Filebeat

•	Go to  /etc/ansible/roles directory and created the ELK playbook (Elk_Playbook.yml)
•	Copy the filebeat-configuration.yml file to /etc/ansible/roles/
•	Update the filebeat-configuration.yml file to include the ELK private IP in lines 1106 and 1806
•	Run the playbook, and navigate to http:// 52.251.40.238/ (ELK-VM public IP) to check that the installation worked as expected

Metricbeat

•	Copy the metricbeat-configuration.yml file to /etc/ansible/roles/files.
•	Update the metricbeat-configuration.yml file to include the ELK private IP in lines 62 and 96.
•	Run the playbook, and navigate to http:// 52.251.40.238:5601/ (ELK-VM public IP) to check that the installation worked as expected.

Additional Validation steps:

•	Run the Elk_Playbook.yml in that same directory (ansible-playbook Elk_Playbook.yml)
•	SSH into the ELK-VM to verify the server is up and running.
•	Check if ELK picking up log data 
•	enter in browser:http://52.251.40.238:5601/app/kibana#/home/tutorial/sysLogs
•	select step 5 on Kibana and check data
•	enter in browser:http://52.251.40.238:5601/app/kibana#/home/tutorial/dockerMetrics
•	select step 5 on Kibana check data
•	Check DVMA 
•	Enter IP address of load balancing or VM 1 or VM 2(should be the same for all 3)
•	Enter User name/Password
•	Verify all IP servers -Jump box IP address
•	Go to gitbash
•	If changed amend: SSH azureuser@XX.X.X.X (IP address changes)
•	cd etc/ansible/roles
•	sudo ansible-playbook pentest.yml

ELK Server monitors the following Machines:

•	NewVM-1 (10.1.0.13) 
•	NewVM-2 (10.1.0.14)
•	Filebeat_playbook.yml
•	Metricbeat_playbook.yml

## Documentation


1. https://kemptechnologies.com/load-balancer/load-balancing-algorithms-techniques/
2. https://docs.microsoft.com/en-us/azure/load-balancer/manage-rules-how-to
3. https://docs.microsoft.com/en-us/learn/browse/
4. https://docs.microsoft.com/en-us/azure/load-balancer/concepts
5. https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/infrastructure-security.html
6. https://en.wikipedia.org/wiki/Jump_server
7. https://www.chaossearch.io/blog/elk-stack-pros-and-cons
8. https://docs.microsoft.com/en-us/azure/governance/policy/overview



