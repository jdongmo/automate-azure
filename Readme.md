# Devops
Ansible repository to perform automatic tasks in Azure cloud.

## Requirements

To run Azure recipe, you should have Azure variable (credentials and
location) set in environment
or having vault file with authentication variables

The host running plays must have python3 installed and library in requirements.txt file
```
pip3 install -r requirements.txt --user
```
The host must also have following packages:
- sshpass
- azure-cli

Give azure credentials in a file *_creds.yml*
```
---
azure_subscription_id: 7ac52367-fb6a-483d-a5ee-c1f218fa0bcc
#Connect using AD account
azure_ad_user: user@domain.tld
azure_password: **************
#Connect using service principal
azure_client_id: a747fc62-38fa-453d-a5fa-ab3039a464cc
azure_secret: *******************************
azure_tenant: 728d20a5-0b44-47dd-9470-20f37cbf2d9a
...
```
And encrypt it with **ansible-vault** 
```
example:
ansible-vault encrypt --vault-password-file  ~/.ssh/creds/vault_password.txt inventory/group_vars/jumpboxes/_creds.yml
```

## Run
To run a playbook, we'll use wrapper script run.sh
To run default infrastructure playbook *infra.yml* who create all the infra
```
./run.sh -v
```
To run another playbook *playbook.yml* after default playbook
```
./run.sh -v playbook.yml
```
To only play another playbook *playbook.yml*
```
ANSIBLE_PLAYBOOK_FILE=playbook.yml ./run.sh -v
```
To only play another playbook (playbook.yml) against specific host *host*
```
ANSIBLE_PLAYBOOK_FILE=playbook.yml ./run.sh -v --limit host
```

## Docker
We have a Dockerfile in order to generate a docker image to use it for
running play in an controled environment.
- Build image: ```docker build -t devops-docker .```
- Run a play using this image:
```
docker run -e -e "ANSIBLE_PLAYBOOK_FILE=playbook.yml" --entrypoint "./run.sh"
devops-docker -v --limit host
```
