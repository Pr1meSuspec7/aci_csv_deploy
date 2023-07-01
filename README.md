
# Cisco ACI deploy from CSV file

This Ansible playbook allows you to manage and deploy ACI objects (Tenant, BD, EPG, etc...) using a CSV file.<br>
In this way you can use a simple csv file to keep updated your infrastructure and track each object, vlan id, subnets, etc...<br>
You can test this playbook on [Cisco ACI Sandbox](https://sandboxapicdc.cisco.com) registering on [Cisco DevNet](https://developer.cisco.com/site/sandbox/).<br>


## Requirements
*  Linux machine (Ubuntu based)
*  Python 3.8
*  Pip
*  Ansible
*  Ansible-galaxy collection cisco.aci


## Setup
**1. Clone this repo:**
```
$ git clone https://github.com/Pr1meSuspec7/aci_csv_deploy.git
$ cd aci_csv_deploy
```

**2. Create and activate python virtualenv:**
```
$ python -m venv venv-ansible
$ source venv-ansible/bin/activate
```

**3. Install ansible and ACI modules:**
```
$ pip install ansible
$ ansible-galaxy collection install cisco.aci
```

## How to use

**1. First of all you have to set up your inventory (inv.ini) and credentials (group_vars/apic.yml):**<br>
- Set in inv.ini file URL or IP of your APIC
- Set in group_vars/apic.yml file username/password of your APIC
> **NOTE**: if you want to test it on [Cisco ACI Sandbox](https://sandboxapicdc.cisco.com) don't touch inv.ini file and retrive login credentials from [Cisco DevNet](https://developer.cisco.com/site/sandbox/) to put in the group_vars/apic.yml file.

<br>

**2. Fill the csv with the EPGs informations:**<br>
- TENANT = name of Tenant
- TENANT_EXIST = [ yes | no ] if "yes" ansible skips the task
- VRF = name of VRF
- VRF_EXIST =  [ yes | no ] if "yes" ansible skips the task
- VRF_PREFERRED = [ enabled | disabled ]
- BD = name of Bridge Domain
- L2_UNKUNICAST = [ proxy | flood ]
- ARP_FLOODING = [ yes | no ]
- ROUTING = [ yes | no ]
- GW = bridge domain ip address
- MASK = bridge domain subnet mask
- GW_PRIMARY = [ yes | no ]
- SUBNET_SCOPE = [ public | private |shared]
- ANP = name of Application Profile
- ANP_EXIST = [ yes | no ] if "yes" ansible skips the task
- EPG = name of EPG
- VLAN_ID = encap vlan for the EPG (this value is entered in the EPG description only)
- DOMAIN_TYPE = [ phys | vmm ]
- DOMAIN = name of Domain
- EPG_PREFERRED = [ yes | no ] Enable or disable EPG preferred group
- PROV_CONTRACT = name of the Provider Contract
- CONS_CONTRACT = name of the Consumer Contract

> **WARNING**: do not touch column headers!

<br>

**3. Test the playbook:**<br>
`$ ansible-playbook playbook.yml --check`
> **NOTE**: with the --check option nothing is configured

<br>

**4. Run the playbook:**<br>
`$ ansible-playbook playbook.yml`


## License

MIT