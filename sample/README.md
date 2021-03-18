![](https://img.shields.io/badge/kube-adm-green)
![](https://img.shields.io/badge/aws-orange)
![](https://img.shields.io/badge/ansible-2.9+-red)
# Ansible Collection - aman_rathi1.kubernetes

## Documentation for the Collection

This collection helps you to create a kubernetes cluster by Kubeadm  on AWS.

This collection contains two roles 

1. awsrole
2. kube_cluster

### **awsrole**

This role helps in launching instances on aws 
For details  about this role read *docs/awsrole.md*

### **kube_cluster**


This role helps in configuring both master and slave, you have to change only the node_name variable.

DO NOT change the default path of the collection if you are doing so, don't forget to provide the new path of collection roles in var *role_path* in *kube_cluster* role.

*node_name: master*       #for configuring master node

*node_name: slave*       #for configuring  slave node

While configuring the master node the token in variable file automatically updated and avaible for slave nodes to be joined, which removes the manual process in between 

for more details about this role read *docs/kube_master.md*  and *kube_slave.md*

Tested on
---------

**Amazon Linux2**

Example 
-------
for launching instances
          
        - hosts: localhost
          remote_user: root
          roles:
	          - aman_rathi1.kubernetes.awsrole

for configuring master node

         - hosts: master 
           vars:
              node_name: master
           roles:
                - { role: aman_rathi1.kubernetes.kube_cluster }    

for configuring slave node
         - hosts: slave 
           vars:
              node_name: slave
           roles:
                - { role: aman_rathi1.kubernetes.kube_cluster } 
For the complete setup use the below playbook

        