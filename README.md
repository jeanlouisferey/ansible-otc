Ansible for Open Telekom Cloud
==============================

Intro
=====

Deutsche Telekom offers since March 2016 an IaaS Service named
Open Telekom Cloud (OTC). The service includes
* Virtual Private Cloud (VPC)
* Elastic Cloud Server (ECS)
* Elastic Load Balancer (ELB)
* Elastic Volume Service (EVS)
and other useful things. The portfolio will rapidly developed.


Content
=======
Here are some roles to demonstrate how to interact with OTC-API.
ECS-API is origin developed by Huawei and described here:
http://support.hwclouds.com/en-us/api/ecs/en-us_topic_0020805967.html

Roles
=====
ecs         list virtual machines
flavors     show flavors
floatingip  show floating ip-addresses
images      show images
job         show job status
keypairs    show keypairs
secgroups   show security groups
subnet      show subnet
token       get auth token
vm          create and start virtual machine
vm_delete   delete a specific virtual machine
vm_info     information about a specific virtual machine
vpc         show vpc

Requirements
============
* Ansible 2.0.1.0
* Ubuntu 14.04.
(should work on all other *nix systems)
* credentials on OTC (username, projectid, generated API key)

Files
=====
* secrets.yml    - var file for OTC credentials and endpoints (ansible-vault)
* vm_secrets.yml - var file for virtual machine conf (ansible-vault)
* vaultpass.txt  - password file for ansible-vault. The default password is: linux :-)
* hosts          - host file for ansible (we use only localhost)

Examples
========

    copy secrets.yml to _secrets.yml and vm_secrets.yml to _vm_secrets.yml 
    with your real data before you using the examples:

show virtual machines

    ansible-playbook -i hosts ecs.yml --vault-password-file vaultpass.txt

show information about a single virtual machines

    ansible-playbook -e "vm_id=f6b7536e-b954-4d73-940f-248de71ce58b vm_name=test06-ansible" -i hosts vm_info.yml --vault-password-file vaultpass.txt

show flavors

    ansible-playbook -i hosts flavors.yml --vault-password-file vaultpass.txt

show floating ip-addresses

    ansible-playbook -i hosts floatingip.yml --vault-password-file vaultpass.txt

show images

    ansible-playbook -i hosts images.yml --vault-password-file vaultpass.txt

show job status

    ansible-playbook -e "job_id=2c9eb2c15693b00901571e32ad5e1755" -i hosts job.yml --vault-password-file vaultpass.txt

show keypairs

    ansible-playbook -i hosts keypairs.yml --vault-password-file vaultpass.txt

show security groups

    ansible-playbook -i hosts secgroups.yml --vault-password-file vaultpass.txt

show subnets

    ansible-playbook -i hosts subnet.yml --vault-password-file vaultpass.txt

show vpc

    ansible-playbook -i hosts vpc.yml --vault-password-file vaultpass.txt

create and start virtual machine (defined in vm_secrets.yml)

    ansible-playbook -i hosts vm.yml --vault-password-file vaultpass.txt

delete virtual machine (only the machine)

    ansible-playbook -e "vm_id=51b6558a-7a6d-49f4-94e5-f4ec94314746 vm_name=test05-ansible" -i hosts vm_delete.yml --vault-password-file vaultpass.txt

delete virtual machine (delete also floating ip and attached volumes)

    ansible-playbook -e "vm_id=f6b7536e-b954-4d73-940f-248de71ce58b vm_name=test06-ansible delete_publicip=1 delete_volume=1" -i hosts vm_delete.yml --vault-password-file vaultpass.txt


Contributing
------------
Very welcome. We are in a very early state of automated platform deployment
on OTC. So each help is still welcome

1. Fork it.
2. Create a branch (`git checkout -b my_markup`)
3. Commit your changes (`git commit -am "Added Snarkdown"`)
4. Push to the branch (`git push origin my_markup`)
5. Open a [Pull Request][1]
6. Enjoy a refreshing Diet Coke and wait

