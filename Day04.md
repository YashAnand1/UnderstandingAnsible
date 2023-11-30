<div align = "center">

# 30 November

</div>

## Study Plan
- Playbooks
- Dry Run
- Loops

## Recap
- Ad Hocs don't have idempotency - modules do - no repeatition 
- Ansible knows work has been done due to 'setup' module which is run first auto when a module is run
- Connect with the 2 VMs again using `ssh ansible@192.168.122.128` and `ssh ansible@192.168.122.46`

## Playbooks
- Collection of modules, which is a collection of config files - one modules does one work
- More work than modules/ad hoc
- In yaml format
- Like a file where you write codes and mention the tasks to be performed. You need the following to create a playbook:
- - Roles (Mandatory)
- - Vars (Mandatory)
- - Tasks (Mandatory)
- - Handlers
- - Files
- - Templates
- Playbooks divided into following sections:
- - Target Section: Define the hosts against which task is to be executed - Mention on what all/<specific group>/<specific node> you want to apply code to
- - Variable Section: Variable is like a wrapper that contains an info - Define variable first and if it's content has to be changed later, change the line where it was defined
- - Task Section: Defines work to be done - lists modules to be run in a order - Ex: install comes before start module 

## YAML Basics 
- For ansible, every YAML starts with a list. They are of equal values or only part of a single group - no multiple parameter:
```
Fruits:
- apple
- banana
- orange
```
- Every item in the list is a list if key-val pair called dictionary like "key: value" - beware of ": "! Ex:
```
---
Customer:
 name: YASH
 job: Student
 skills: Ansible
```
- Every YAML has to start with "---" optionally end with "..." & format = ".yml/.yaml"
- Every members of a list must begin with same indentation & "-":
```
task:
    - work:
        - abc
task:
    - work:
        - xyz
```
## Creating Playbook
- Create a YAML file with '.yaml/.yml' on ansible server:
```
---
- hosts: demoByYash
- user: ansible 
- become: yes # for sudo connection
- connection: ssh # target section till here
- gather_facts: yes # task section, these are done by itself but to display these using the playbook
...
```
- Execute the playbook using `ansible-playbook <playbook>.yml`


## Creating Playbook
```
---
- name: Get current target host's IP address using shell command
  hosts: demoByYash
  connection: ssh
  gather_facts: yes

  tasks:
    - name: Fetch IP address using shell command
      vars:
        command: "hostname -I | awk '{print $1}'"
      shell: "{{ command }}"
      register: ip_address_result

    - name: Display the IP address
      debug:
        var: ip_address_result.stdout
```
Reference: [Link](https://www.educative.io/answers/how-to-get-current-target-hosts-ip-address-in-ansible)
