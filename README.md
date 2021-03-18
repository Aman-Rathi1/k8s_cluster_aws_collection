![](https://img.shields.io/badge/kube-adm-green)
![](https://img.shields.io/badge/aws-orange)
![](https://img.shields.io/badge/ansible-2.9+-red)
# Ansible Collection - aman_rathi1.kubernetes

## Documentation for the Collection

This collection helps you to create a kubernetes cluster by Kubeadm  on AWS.

This collection contains two roles 

1. awsrole
2. kube_cluster



awsrole
=========

This roles helps to launch instances on aws cloud al you need to do is follow below steps
1. Configure the ansible.cfg like this
 
       [defaults]
       host_key_checking = false
       remote_user: "username"
       private_key_file = "location of private key"

       [privilege_escalation]
       become = true
       become_method = sudo
       become_user = root
       become_ssh_pass = false

2. Install the given requirements
3. Download the ec2.py and ec2.ini and make them executable (this will dynamically fetch the hosts from aws)
4. Set the credential of aws by the using below commands
   
       $ export AWS_ACCESS_KEY_ID='YOUR_AWS_API_KEY'
       $ export AWS_SECRET_ACCESS_KEY='YOUR_AWS_API_SECRET_KEY'

for additional information related to ec2_module refer (https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_module.html)




Requirements
------------
*python3*

*boto (2.49.0)*

*boto3 (1.14.45)*

*botocore(1.17.45)*

*ec2.py*

*ec2.ini*



Role Variables
--------------


key_name: ""

instance_type: ""

ami_id: ""

wait: yes

subnet_id: ""

assign_ip: yes

region: ""

state: present

security_group: ""

tag_name: ""             #tagging the instances

count: ""                #no of instances to launch 

These are the variables to be set in vars/main.yml


Example Playbook
----------------

This playbook launch 

    - hosts: localhost
      roles:
         - { role: amanrathi1.awsrole }



![](https://img.shields.io/badge/kubernetes-masternode-green) 

Kube_cluster
=========

This role helps in configuring both master and slave, you have to change only the node_name variable.

DO NOT change the default path of the collection if you are doing so, don't forget to provide the new path of collection roles in var *role_path* in *kube_cluster* role.

*node_name: master*       #for configuring master node

*node_name: slave*       #for configuring  slave node

While configuring the master node the token in variable file automatically updated and avaible for slave nodes to be joined, which removes the manual process in between  

Requirements
------------

NONE

Role Variables
--------------

node_name

network_cidr    #don't  change default one if you are using official flannel cni 

While configuring master the token variable will be automatically updated for future use


Dependencies
------------

NONE

Example Playbook
----------------

example  to configure master node

    - hosts: master
      vars:
        node_name: master
      roles:
         - { role: amanrathi1.kubernetes.kube_cluster }


example  to configure slave node

    - hosts: slave
      vars:
        node_name: slave
      roles:
         - { role: amanrathi1.kubernetes.kube_cluster }



Tested on
---------

**Amazon Linux2**

Example 
-------
Compelte playbook for using this collection
          

             - hosts: localhost
               vars:
                  key_name: ""
                  instance_type: ""
                  ami_id: ""
                  wait: yes
                  subnet_id: ""
                  assign_ip: yes
                  region: ""
                  state: present
                  security_group: ""
                  tag_name: master
                  count: 1
               tasks:
               - name: launching master nodes   
                 include_role:
                    role: aman_rathi1.kubernetes.awsrole

 
             - hosts: localhost
               vars:
                   key_name: ""
                   instance_type: ""
                   ami_id: ""
                   wait: yes
                   subnet_id: ""
                   assign_ip: yes
                   region: ""
                   state: present
                   security_group: ""
                   tag_name: slave
                   count: 1
               tasks:
               - name: launching slave nodes
                 include_role:
                    name: aman_rathi1.kubernetes.awsrole
               - name: refreshing inventory
                 meta: "refresh_inventory"


             - hosts: tag_name_master
               vars:
                  node_name: master
               tasks:
               - name: configuring master
                 include_role:
                     name: aman_rathi1.kubernetes.kube_cluster


             - hosts: tag_name_slave
               vars:
                  node_name: slave
               tasks:
               - name: configuring slave
                  include_role:
                      name: aman_rathi1.kubernetes.kube_cluster
   
this role you can find in **sample/main.yml**

 Author Information
------------------
linkedin   *https://www.linkedin.com/in/aman-rathi-76b72b1a1/*

github *https://github.com/Aman-Rathi1/*       