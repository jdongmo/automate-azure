#Resource Group
This is a quick howto on resource group playbook

##Variables
```
---
rgs:
  - name:
    location:
    force_delete:
    state:
    tags:
      "env": "prod"
      "provisioner": "ansible"
...
```

##Commands

- List resource group
```
ANSIBLE_PLAYBOOK_FILE=playbook_resource_group.yml ./run.sh -vv -e "{rgs: [{name: 'jdongmohub-nonprod-eca1-gen-rg01', location: 'canadaeast'}]}"  -e action="list"
```

- Create resource group
```
ANSIBLE_PLAYBOOK_FILE=playbook_resource_group.yml ./run.sh -vv -e "{rgs: [{name: 'jdongmohub-nonprod-eca1-gen-rg01', location: 'canadaeast', state: 'present'}]}"
```

- Delete resource group containing resources
```
ANSIBLE_PLAYBOOK_FILE=playbook_resource_group.yml ./run.sh -vv -e "{rgs: [{name: 'jdongmohub-nonprod-eca1-gen-rg01', force_delete: true}]}" -e action="absent"
```
