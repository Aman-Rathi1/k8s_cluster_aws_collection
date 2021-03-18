Role Name
=========

This roles helps to launch instances on aws cloud al you need to do is folloe below steps
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
python3
boto (2.49.0)
boto3 (1.14.45)
botocore(1.17.45)

ec2.py 
ec2.ini


Role Variables
--------------
key_name: ""                                                                                                                                        instance_type: ""                                                                                                                                   ami_id: ""                                                                                                                                          wait: yes                                                                                                                                           subnet_id: ""                                                                                                                                       assign_ip: yes                                                                                                                                      region: ""                                                                                                                                          state: present                                                                                                                                      security_group: ""
tag_name: ""             #tagging the instances
count: ""                #no of instances to launch 

These are the variables to be set in vars/main.yml


Example Playbook
----------------

This playbook launch 

    - hosts: localhost
      roles:
         - { role: amanrathi1.awsrole }

License
-------	

BSD

Author Information
------------------
github (https://github.com/Aman-Rathi1/)
