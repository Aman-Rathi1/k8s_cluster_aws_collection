![](https://img.shields.io/badge/kubernetes-slavenode-red) 

Kube_cluster
=========

This role helps to configure both master and slave only we have to provide the (node_name: master) for configuring master nodes and (node_name: slave) for configuring worker or slave nodes.

Requirements
------------

NONE

Role Variables
--------------

node_name

network_cidr    #don't  change default one if you are using official flannel cni 

token
This variable is available in token.yml file in vars dir

Dependencies
------------

NONE

Example Playbook
----------------

example how to configure slave node

    - hosts: slave
      vars:
        node_name: slave
      roles:
         - { role: amanrathi1.kubernetes.kube_cluster }

License
-------

BSD

Author Information
------------------
https://www.linkedin.com/in/aman-rathi-76b72b1a1/
