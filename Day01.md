<div align = "center"> 

  # 27 November, 2023

</div>

## References
- [ANSIBLE-CMDB Docs](https://ansible-cmdb.readthedocs.io/en/latest/usage/) 
- [ANSIBLE THEORY](https://www.youtube.com/watch?v=75wa1N49b-o&list=PLBGx66SQNZ8aPsFDwb79JrS2KQBTIZo10&index=32)
- [ANSIBLE-CMDB Use Case](https://www.reddit.com/r/ansible/comments/7op6wq/what_configuration_management_tool/)
- [Push & Pull in Config Man](https://gayatrisajith.medium.com/beginner-fundamentals-push-pull-configuration-management-tools-85eff1b41447)

## Today's plan:
1. Gain basics of Ansible-CMDB 
2. Gain basics of Ansible
3. Prioritise Ansible theory

## Ansible-CMDB Intro
- CMDB = Config Management DB
- It takes output of ansible's fact gathering
- converts it into static html overview, containing config info
- It supports html, csv, txt, sql, etc. outputs
- Extension of Ansible

## Ansible
- Redhat's new configuration management tool like puppet/chef (Has GUI Ansible-Tower
- System admin manages all servers (manuallu installs/updates softwares)
- Has a push process/mechanism, sends notification to all servers that you need to update, only updates when needed
- YAML scripting used for using Ansible, Uses key-pair

## ANSIBLE EXTRA
- if mass install/update has to take place on 100s of servers, ansible can manage many servers 
- Many servers can be managed at once with this config man tool, no need for manually managing servers individually
- A device's ram, soft installed, ip, etc. are configs, management is deleting, adding, etc is manageemnt - ansible does these
- ansible = a device for instantaneous communication
- PUSH MECHANISM MOST IMPORTANT - no need to know prog lang - Means user will be the one sending notif to update/install
- can be used for physical, vm, cloud servers
- conf mans turn code into infra (IAC: Infra As Code), write the kind of infra you want as code and ansible'll configure on server on its own

## Architecture of Ansible
- ANSIBLE SERVER directly communicates with servers to be configed 
- Push mechanism - analogy: Doesnt go and ask continuously if work is there, waits for request - not active worker, waits for boss to give order
- NOT 100% AUTOMATION - PUSH has to be made by user!
- YAML - Yet ANother Markup Lang - Human readable
- AGENTLESS - VERY IMPORTANT - NO NEED TO INSTALL ANYTHING! - Talks through SSH (keygen) with the servers 
- You write scripts in playbook, where modules = resources, available online

## Features
| Advantages |
|------------|
|Free to use: OSS|
| Highly secure: agentless & ssh |
|Lightweight | 
| YAML: Special training not needed |
| Push Mechanism |
_______________________________
