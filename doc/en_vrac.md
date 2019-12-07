# En vrac

## Availability set
```
ANSIBLE_PLAYBOOK_FILE=playbook_availability_set.yml ./run.sh -vv -e "{avss: [{name: 'jdongmohub-eca1-gen-avs01', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', platform_fault_domain_count: 2, platform_update_domain_count: 2, sku: 'Aligned', state: 'present'}]}"
```

## Storage account
```
ANSIBLE_PLAYBOOK_FILE=playbook_storage_account.yml ./run.sh -vv -e "{sas: [{name: 'jdongmohubeca1gensa01', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', access_tier: 'Hot', account_type: 'Standard_LRS', blob_cors: [], force_delete_nonempty: true, https_only: true, kind: 'StorageV2', state: 'present', tags: {'env': 'test', 'provisioner': 'ansible'}}]}"
```

## Log analytics workspace
```
ANSIBLE_PLAYBOOK_FILE=playbook_analytics_workspace.yml ./run.sh -vv -e "{laws: [{name: 'jdongmohub-eca1-gen-ngfw-law01', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', location: 'canadacentral', retention_in_days: 90, state: 'present'}]}"
```

## sentinel
```
ANSIBLE_PLAYBOOK_FILE=playbook_sentinel.yml ./run.sh -vv -e "{sentinels: [{law: {name: 'jdongmohub-eca1-gen-ngfw-law01', subscriptionid: 'd89d587d-8a3f-4e4d-ac5a-636b4aa7b5d8'}, resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', location: 'canadacentral', state: 'present'}]}"
```

## Routing table
```
ANSIBLE_PLAYBOOK_FILE=playbook_routing_table.yml ./run.sh -vv -e "{rts: [{name: 'jdongmohub-eca1-gw-rt', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', disable_bgp_route_propagation: false, state: 'present'}, {name: 'jdongmohub-eca1-sub01-rt', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', state: 'present'}, {name: 'jdongmohub-eca1-sub02-rt', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', state: 'present'}]}"
```

## Network security group
```
ANSIBLE_PLAYBOOK_FILE=playbook_network_security_group.yml ./run.sh -vv -e "{nsgs: [{name: 'jdongmohub-eca1-nsg01', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', purge_rules: true, rules: [{name: 'Allowtcp22', description: 'Allow incoming tcp traffic on port 22', protocol: 'Tcp', destination_port_range: 22, access: 'Allow', direction: 'Inbound', priority: 122}, {name: 'Allowtcp443', description: 'Allow incoming tcp traffic on port 443', protocol: 'Tcp', destination_port_range: 443, access: 'Allow', direction: 'Inbound', priority: 443}], state: 'present'}]}"
```

## Subnet
```
ANSIBLE_PLAYBOOK_FILE=playbook_subnet.yml ./run.sh -vv -e "{subnets: [{name: 'GatewaySubnet', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', virtual_network_name: 'jdongmohub-eca1-gen-vnet01', address_prefix_cidr: '10.225.135.0/28', route_table: 'jdongmohub-eca1-gw-rt', state: 'present'}, {name: 'jdongmohub-eca1-mgt-sub01', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', virtual_network_name: 'jdongmohub-eca1-gen-vnet01', address_prefix_cidr: '10.220.135.0/28', route_table: 'jdongmohub-eca1-sub01-rt', state: 'present'}]}"
ANSIBLE_PLAYBOOK_FILE=playbook_subnet.yml ./run.sh -vv -e "{subnets: [{name: 'jdongmohub-eca1-trust-prod-sub02', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', virtual_network_name: 'jdongmohub-eca1-gen-vnet01', address_prefix_cidr: '10.225.135.16/28', route_table: 'jdongmohub-eca1-sub02-rt', state: 'present'}]}"
```
```yaml
subnets:
  - name: 'GatewaySubnet'
    resource_group: 'jdongmohub-nonprod-eca1-gen-rg01'
    virtual_network_name: 'jdongmohub-eca1-gen-vnet01'
    address_prefix_cidr: '10.225.135.0/28'
    route_table: 'jdongmohub-eca1-gw-rt'
    state: 'present'
  - name: 'jdongmohub-eca1-mgt-sub01'
    resource_group: 'jdongmohub-nonprod-eca1-gen-rg01'
    virtual_network_name: 'jdongmohub-eca1-gen-vnet01'
    address_prefix_cidr: '10.220.135.0/28'
    route_table: 'jdongmohub-eca1-sub01-rt'
    state: 'present'
  - name: 'jdongmohub-eca1-trust-prod-sub02'
    resource_group: 'jdongmohub-nonprod-eca1-gen-rg01'
    virtual_network_name: 'jdongmohub-eca1-gen-vnet01'
    address_prefix_cidr: '10.225.135.16/28'
    route_table: 'jdongmohub-eca1-sub02-rt'
    state: 'present'
  - name: 'jdongmohub-eca1-trust-nprod-sub03'
    resource_group: 'jdongmohub-nonprod-eca1-gen-rg01'
    virtual_network_name: 'jdongmohub-eca1-gen-vnet01'
    address_prefix_cidr: '10.220.135.16/28'
    route_table: 'jdongmohub-eca1-sub03-rt'
    state: 'present'
  - name: 'jdongmohub-eca1-untrust-prod-sub04'
    resource_group: 'jdongmohub-nonprod-eca1-gen-rg01'
    virtual_network_name: 'jdongmohub-eca1-gen-vnet01'
    address_prefix_cidr: '10.225.135.32/28'
    route_table: 'jdongmohub-eca1-sub04-rt'
    state: 'present'
  - name: 'jdongmohub-eca1-untrust-nprod-sub05'
    resource_group: 'jdongmohub-nonprod-eca1-gen-rg01'
    virtual_network_name: 'jdongmohub-eca1-gen-vnet01'
    address_prefix_cidr: '10.220.135.32/28'
    route_table: 'jdongmohub-eca1-sub05-rt'
    state: 'present'

```

## Network interface card
```
ANSIBLE_PLAYBOOK_FILE=playbook_network_interface_card.yml ./run.sh -vv -e "{nics: [{name: 'jdongmohub-eca1-mgt-nic01', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', create_with_security_group: true, enable_accelerated_networking: false, enable_ip_forwarding: false, security_group: 'jdongmohub-eca1-nsg01', subnet_name: 'jdongmohub-eca1-mgt-sub01', virtual_network: 'jdongmohub-eca1-gen-vnet01', state: 'present'}, {name: 'jdongmohub-eca1-trust-prod-nic02', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', create_with_security_group: true, enable_accelerated_networking: false, enable_ip_forwarding: false, security_group: 'jdongmohub-eca1-nsg01', subnet_name: 'jdongmohub-eca1-trust-prod-sub02', virtual_network: 'jdongmohub-eca1-gen-vnet01', state: 'present'}]}"
```
```yaml
nics:
  - name: "jdongmohub-eca1-mgt-nic01"
    dns_servers: []
    create_with_security_group: true
    enable_accelerated_networking: false
    enable_ip_forwarding: false
    resource_group: "{{ base_name }}-rg01"
    security_group: "{{ base_name }}-allowtcp22"
    subnet_name: "spi-dns-caea-sim-ssh-subnet01"
    virtual_network: 'jdongmohub-eca1-gen-vnet01'
    state: "present"
  - name: "jdongmohub-eca1-trust-prod-nic02"
    dns_servers: []
    create_with_security_group: true
    enable_accelerated_networking: false
    enable_ip_forwarding: false
    resource_group: "jdongmohub-nonprod-eca1-gen-rg01"
    security_group: "jdongmohub-eca1-nsg01"
    subnet_name: ""
    virtual_network:
      name: ""
      resource_group: ""
    state: "present"
    tags:
      "env": "test"
      "provisioner": "ansible"
```

## User defined route
```
```

## Virtual machine
```
ANSIBLE_PLAYBOOK_FILE=playbook_virtual_machine.yml ./run.sh -vv -e "{vms: [{name: 'jdongmohub-eca1-relay-vm01', resource_group: 'jdongmohub-nonprod-eca1-gen-rg01', network_interfaces: ['jdongmohub-eca1-trust-prod-nic02'], managed_disk_type: 'StandardSSD_LRS', os_disk_size_gb: 200, ip_allocation: 'Disabled', remove_on_absent: ['virtual_storage'], restarted: false, ssh_password_enabled: true, storage_account_name: 'jdongmohubeca1gensa01', subnet_name: 'jdongmohub-eca1-trust-prod-sub02', virtual_network: 'jdongmohub-eca1-gen-vnet01', vm_size: 'Standard_B1s', image: {publisher: 'OpenLogic', offer: 'CentOS', sku: '7.1', version: 'latest'}, admin_username: 'admin', admin_password: '********', state: 'present'}]}" 
```
```yaml
vms:
  - name: "{{ base_name }}-vm-syslog"
    admin_username: admin
    admin_password: ********
    image:
      publisher: 'OpenLogic'
      offer: "CentOS"
      sku: '7.1'
      version: 'latest'
    resource_group: '{{ base_name }}-rg01'
    network_interfaces:
      - "{{ base_name }}-nic06"
    managed_disk_type: "StandardSSD_LRS"
    os_disk_size_gb: 500
    ip_allocation: "Disabled"
    remove_on_absent:
      - "virtual_storage"
    restarted: false
    ssh_password_enabled: true
    storage_account_name: 'jdongmocaeasa03'
    subnet_name: "spi-dns-caea-sim-ssh-subnet01"
    virtual_network: "spi-dns-caea-sim-vnet01"
    vm_size: 'Standard_B1s'
    state: 'present'
    tags:
      "env": "jdongmo"
      "provisioner": "ansible"
```

## Load balancer
```
```
