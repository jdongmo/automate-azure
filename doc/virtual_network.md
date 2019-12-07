#Resource Group
This is a quick howto on resource group playbook

##Variables
```
---
vnets:
  - name:
    address_prefixes_cidr: []
    dns_servers:
    location:
    purge_address_prefixes:
    resource_group:
    state:
    tags:
      "env": "prod"
      "provisioner": "ansible"
...
```

##Commands

- List virtual network
```
ANSIBLE_PLAYBOOK_FILE=playbook_virtual_network.yml ./run.sh -vv -e "{vnets: [{name: '', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01'}]}"  -e action="list"
```

- Create virtual network
```
ANSIBLE_PLAYBOOK_FILE=playbook_virtual_network.yml ./run.sh -vv -e "{vnets: [{name: 'jdongmohub-nonprod-eca1-gen-vnet01', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', address_prefixes_cidr: ["10.220.135.0/25", "10.225.135.0/25"], location: 'canadaeast', state: 'present'}]}"
```

- Delete virtual network
```
ANSIBLE_PLAYBOOK_FILE=playbook_virtual_network.yml ./run.sh -vv -e "{vnets: [{name: 'jdongmohub-nonprod-eca1-gen-vnet01', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', state: 'absent'}]}"
```
