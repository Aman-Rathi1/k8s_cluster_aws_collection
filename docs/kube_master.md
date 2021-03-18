![](https://img.shields.io/badge/kubernetes-masternode-green) 

Kube_cluster
=========

This role helps to configure  master node 

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

example how to configure master node

    - hosts: master
      vars:
        node_name: master
      roles:
         - { role: amanrathi1.kubernetes.kube_cluster }

License
-------

BSD

Author Information
------------------
linkedin   *https://www.linkedin.com/in/aman-rathi-76b72b1a1/*

github *https://github.com/Aman-Rathi1/*
