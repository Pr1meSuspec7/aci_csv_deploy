
# Cisco ACI deploy from CSV file

This is an Ansible script that can help you to deploy many object starting from a CSV file.

## Requirements
*  Python 3.8
*  Ansible
*  Paramiko


## How to use
1- Before all you have to set up your inventory file (inv.ini) and credentials file (group_vars/apic.yml).
2- In the "playbook.yml" change lines 70,71 with the correct "Domain" and "Domain Type" you want to use.
3- In the main folder there is a CSV file called "epg_list.csv" which contains some columns:

VLAN_ID | VLAN_NAME | EPG | ANP | BD | VRF | TENANT
------- | --------- | --- | --- | -- | --- | ------


**WARNING**: You should not change these keys, if you do this you have to make some changes in the ansible playbook.


4- Fill the csv with the EPGs informations...
Example:

VLAN_ID | VLAN_NAME | EPG 			| ANP 		| BD 		   | VRF 	   | TENANT
------- | --------- | ------------- | --------- | ------------ | --------- | ------
10		| myapp-web | myapp-web_epg | myapp_anp | myapp-web_bd | myapp_vrf | PROD
20		| myapp-app | myapp-app_epg | myapp_anp | myapp-app_bd | myapp_vrf | PROD
30		| myapp-db  | myapp-db_epg  | myapp_anp | myapp-db_bd  | myapp_vrf | PROD

5- Run the playbook:
`$ ansible-playbook playbook.yml`


**NOTE**: Before run you have to be sure the tenant exist because the playbook don't create tenants.