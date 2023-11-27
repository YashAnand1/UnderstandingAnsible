<div align = "center"> 

  # 27 November, 2023

</div>

## Today's plan:
1. Gain basics of Ansible-CMDB 
2. Gain basics of Ansible
3. Prioritise Ansible theory

## Ansible-CMDB Introduction
- CMDB = Config Management DB
- It takes output of ansible's fact gathering
- Converts it into static html overview, containing config information
- It supports html, csv, txt, sql, etc. outputs
- Extension of Ansible

## Ansible Introduction
- Redhat's new configuration management tool like puppet/chef (Has GUI Ansible-Tower)
- System admin manages all servers (manuallu installs/updates softwares)
- Has a push process/mechanism, sends notification to all servers that you need to update, only updates when needed
- YAML scripting used for using Ansible, Uses key-pair
- Ansible can manage many servers if mass install/update has to take place on 100s of servers at once
- No need for manually managing servers individually
- Configurations = RAM, softwares installed, IP, etc. | Management = deleting, adding, etc. of configurations
- Ansible = a device for instantaneous communism
- PUSH MECHANISM MOST IMPORTANT - User will be the one sending signals to update, install, etc.
- Can be used for Physical, VM, Cloud servers
- Configuration management turns code into infra (IAC: Infra As Code) - write the kind of infra you want as code - Ansible will configure server on its own

<div align = "center"> 
  
| Advantages |
|------------|
|Free to use: OSS|
| Highly secure: agentless & ssh |
|Lightweight | 
| YAML: Special training not needed |
| Push Mechanism |
  
</div>

## Architecture of Ansible
- ANSIBLE SERVER directly communicates with servers to be configed
- NOT 100% AUTOMATION - PUSH has to be made by user!
- YAML - Yet ANother Markup Lang - Human readable - Push mechanism
- AGENTLESS - VERY IMPORTANT - NO NEED TO INSTALL ANYTHING! - Talks through SSH with the servers 
- You write scripts in playbook, where modules = resources, available online

## References
- [ANSIBLE-CMDB Docs](https://ansible-cmdb.readthedocs.io/en/latest/usage/) 
- [ANSIBLE THEORY](https://www.youtube.com/watch?v=75wa1N49b-o&list=PLBGx66SQNZ8aPsFDwb79JrS2KQBTIZo10&index=32)
- [ANSIBLE-CMDB Use Case](https://www.reddit.com/r/ansible/comments/7op6wq/what_configuration_management_tool/)
- [Push & Pull in Config Man](https://gayatrisajith.medium.com/beginner-fundamentals-push-pull-configuration-management-tools-85eff1b41447)

_______________________________

Note to self: Try to come up with analogies for better understanding. 
