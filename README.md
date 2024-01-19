<div align="center">
  
# 🪐 UNDERSTANDING ANSIBLE 🪐    
# — Daily Progress-Logging For Self-Monitoring —    

_____________________________________________________________________________________                        

### 📚 Contents 📚
</div>

- [Overview](#overview)
- [Logs](#logs)
_____________________________________________________________________________________      

<div align="center">
   
## 🪐 **Overview** 🪐 
</div>


Greetings from 27/11/2023 and welcome to the Ansible documentation repository which I have set up in order to closely track my everyday's progress towards learning Ansible. 

| **Please note that the updates added to this repository are for my own reference for helping me monitor my own upskilling. However, I do plan on sharing them in case it is required for me to share my day's contribution in detail.** |
|----------|

This document is to act like a log of my daily contributions towards understanding Ansible and Ansible-CMDB. Though the daily updates will be written for my own self-reference, they can also be used as a reference for others who may want to look into the contributions that I have made per day.

_____________________________________________________________________________________   

<div align="center">

## 🪵 **Declaration of Logs** 🪵 
</div>

The daily updates or logs will be written everyday and pushed to this repository using Git. In case of missed updates, I will be trying to publish them the next day. 

These logs can be accessed by going through the index provided in this repository. For reference, these daily logs can also be attached with the daily updates mails that are sent from my side to my Team Leader.

______________________________________________________________________________________

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
______________________________________


<div align = "center">

# 28 November

</div>

# References
- [ANSIBLE DEMO](https://www.youtube.com/watch?v=kE-6KDyf-0o&list=PLBGx66SQNZ8aPsFDwb79JrS2KQBTIZo10&index=32)
- [Installing ANSIBLE](https://phoenixnap.com/kb/install-ansible-ubuntu-20-04)

# Today's plan:
1. Create an ansible server & 2 nodes
2. Establishing connection

# Setting up servers
- We create the server ec2 instance 
- download package using wget & then install ansible server'spackage
- epel = extra paxkages for enterprise linux 
- To create shahee paneer/a dish we bought the ingredients by installing the main ingredient/paneer/ansible
- we need to install other dependencies/components to create a dish - these dishes are part of the package
- How will ansible server know what nodes are connected with it - what nodes it has to send updates to
- In ansible server, find ivnentory file/host default file, enter pvt ip of nodes for saving it to let server know who it is connected with "vi /etc/ansible/hosts"
- Inside the file, create a "demo group" and paste node1 & 2 pvt ip
- another file in ansible: config file where commands are written but //ed, remove // before inventory & inventory file activated! also remove // before sudo-user = root
- connection still not established b/w nodes & ansible server - we create 3 ansible users in the nodes as root user won't be known for each node practically
- "adduser user/ansible" in 3 servers, setting passwords using "passwd user/ansible"
- switching users in servers with switch user with su - ansible
- giving root privelege to ansible by editing visudo file, add:
ansible ALL=(ALL) NOPASSWD:ALL
- STILL have to write commands w/ sudo since you are not root user - ansible user is only a sudo user not root user
- NO communication b/w servers through ssh, come bacck to ansible server and we need to install ssh 
- make changes to /etc/ssh/sshd_config & node 1 and node 2 should be allowed to connect
- create the connection in the server by creating 
- sudo apt-get install ansible
got erro "sudo ansible --version
ERROR: Ansible requires the locale encoding to be UTF-8; Detected ISO8859-1." after installing
solved by https://www.reddit.com/r/ansible/comments/z66t0l/comment/jwenrji/?utm_source=share&utm_medium=web2x&context=3 adding following to .bashrc:
```
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8
```

- work as an ansible user and create necessary 
- ansible --version shows "config file = /etc/ansible/ansible.cfg" 
- the hosts file will not work until we make chanes to ansible.cfg

- nano /etc/ansible/hosts
created a group including my vm called "demoByYash" using:
[demoByYash]
192.168.122.128

- vi /etc/ansible/ansible.cfg and uncommented "$ ansible-config init --disabled > ansible.cfg"

- there are only 2 files in /etc/ansible. my ansible.cfg says:
```
# Since Ansible 2.12 (core):
# To generate an example config file (a "disabled" one with all default settings, commented out):
#               $ ansible-config init --disabled > ansible.cfg
#
# Also you can now have a more complete file by including existing plugins:
# ansible-config init --disabled -t all > ansible.cfg

# For previous versions of Ansible you can check for examples in the 'stable' branches of each version
# Note that this file was always incomplete  and lagging changes to configuration settings

# for example, for 2.9: https://github.com/ansible/ansible/blob/stable-2.9/examples/ansible.cfg
```
so i ran ansible-config init --disabled -t all > ansible.cfg

- adduser ansible in both machines

- su - ansible for switching to the new user

- i got an error when trying to test install httpd "sudo apt install httpd
[sudo] password for ansible: 
ansible is not in the sudoers file.
This incident has been reported to the administrator."

- to create it same as root user, i logged out of ansible user on BOTH SERVERS and ran "visudo", under the "allow root to run any commands anywhere", I addded the following:
```
ansible ALL=(ALL)   NOPASSWD: ALL
```
- TO CHECK if connection has been established b/w node & server, come to server and run su - ansible and establish ssh between the 2 USERS

- when i ran ssh 192.168.122.128, i was able to connect with the node from my server

optional i think:
- changes made to /etc/ssh/sshd_config in both servers:
1. added this line: PermitRootLogin yes
2. uncommented PasswordAuthentication yes
3. outside of the file ran service sshd restart

- to verify the connection, turn ansible user first, establish ssh connection

- if i had another node, i'd have to connect to 2nd node from main server again - since i have to enter password again and again while trying to establish connection with ssh, I have to remove password authentication - not practical since we have to update 100s of server, automation with password is not feasible

- solution, we gen a key inside ansible server using ssh keygen, one pub and one pvt, it is imp to be signed in as same level user in all servers - when creating trust relation, you need gen ssh-keygen seen using ls -a

- inside .ssh i'd see id_rsa and id_rsa_pub and when you connect using ansible@ip again, you'll be asked to enter passwd first only - 

- inside the server, add the public key on the node so that node always knows that the server is authenticate - everything to be done as an ansible user 

- first in server, run "ssh-keygen" - do ls -a and you'll find .ssh, inside is id_rsa and id_rsa.pub, copy the public key

- to copy public key to node, we run "ssh-copy-id ansible@192.168.122.12 - for the last time passwd is asked and once done, connection will be set w/o passwd

- in the nodes server, ~/.ssh/authorized_keys get created and the
id_rsa.pub is added form the server - automatically after running ssh-copy-id on the server

**[Host Pattern](https://blog.knoldus.com/working-of-adhoc-commands-and-modules-in-ansible/)**
- lets say ansible server connected w/ 10 nodes
- We won't need to always run updates on all nodes at once, may have to update only the 1st server or 5 servers
- We may want to update specific groups from inventory file (remember we made [demoByYash] group and added 1 node to it
- "all" pattern means talking about all nodes in the inventory/hosts file
- GROUP
- "ansible all --list-hosts" to check all connected nodes
0. In ansible, nodes start from 0. node 1 = 0, node 3 = 2 - to find from last do -1 for last, -2 for second last node
1. "ansible <group name> [0] --ansible-hosts" would give first node 2. "ansible <group name> [1] --ansible-hosts" to give second node
3. "ansible <group name> [1:5] -- ansible-hosts" to range b/w 1 & 5
4. "ansible <group name> [-1] --ansible-hosts" to give last node
5. lets say there are 2 groups, demoByYash and devops and you want to find data b/w a range:
"ansible demoByYash[1:5]:devops[0:3]

- Practical:
- - To find the first node, i ran: "ansible demoByYash[0] --list-hosts" - where 0 is denoted by the first node
- - Since there is only one node, "ansible demoByYash[1] --list-hosts" gives "[WARNING]: No hosts matched, nothing to do
  hosts (0):"

Conclusion:
- 3 servers: 1 ansible server other 2 node servers
- Connection b/w the 3 established, after server installed with "sudo apt-get install ansible"
- In /etc/ansible/, ansible.cfg & hosts/inventory files exist, enter IP of nodes in hosts under a group like [group]\nIP
- User created in 3 servers and given sudo priv using visudo, don't want to talk as root user, su - ansible from now on, ansible user could now update/install things on server
- in sshd_config, made changes to allow server to push/install files & connect w/ nodes
- ssh-keygen in server as user ansible and ssh-copy-id nodeuser@nodeip so passwd not asked again
- host patterns:
1. ansible --all --list-hosts
2. ansible <group>[0] --list-hosts for first node
3. ansible <group>[-1] --list-hosts for last node
4. ansible <group>[0:4] --list-hosts for ranged nodes
__________________________

<div align = "center">

# 29 November

</div>

## References
- [ANSIBLE AD HOC, Modules and Playbooks](https://www.youtube.com/watch?v=SR_CZcZQfqE&list=PLBGx66SQNZ8aPsFDwb79JrS2KQBTIZo10&index=33)
- [Ansible Ad Hoc Document](https://docs.ansible.com/ansible/latest/command_guide/intro_adhoc.html)

## Today's plan:
- Ad hoc, Modules, Playbook

## Ways of pushing
- Ad hoc commands
- Modules
- Playbook

| Ad Hoc | Modules | Playbooks | 
|----------|---------|---------|
| Simple linux commands | Written in YAML | Written in YAML |
| Ad Hoc in eng = temp/emergency/improvised | If a single cmd to be written, its a module | Collection of Modules - more than 1 module |
| SOmething used for immediate purpose | Single work | Like a collection of pages: BOOK |
| BAD BECAUSE IT OVERWRITES! If "touch abcd1" run twice, v1 is overwritten | Like a page | Does more work |
| Ex: "adduser abcd" | Ex: Gotta run "sudo apt update" | Ex: Gotta update system, install sudo apt get ims, start the server, start etcd |

**NOTE:** Modules & Playbooks check if the user has already AND THEN create it, no overwriting.

# Ad Hoc
- [Ansible ad-hoc means running tasks using the Ansible command, not playbooks. (Ansible-playbook command). You would typically do this when you need to test Ansible connectivity(ping module), test something like a filter or look at host facts(setup module)](https://www.reddit.com/r/redhat/comments/hnbcia/comment/fxae6bu/?utm_source=share&utm_medium=web2x&context=3)
- Simple linux commands, used as temp measure for immediate need when playbooks/modules aren't known
- WHY USE PLAYBOOKS WHEN AD HOCS ARE DOING THE PUSHING? - Have no idempotency - ad hocs change result on repeat: [It means you can keep performing the operation over and over again and it gives you the same value as the first time you called it.](https://www.reddit.com/r/explainlikeimfive/comments/54u529/comment/d84zg7c/?utm_source=share&utm_medium=web2x&context=3) - Ex: touch file1 and repeat command, file overwritten- same commands can be repeated
- Ex: starting all machine, creating a small 100s of files on 100s of servers
- Used for INDIVIDUAL quick short work - not reliable for complex work 
- Not used for config management & deployment bcs of their one time usage
- Ad hoc uses command ansible's cmd line tool found in /usr/bin/ansible to automate single task
- BY default "-m command" silently added b/w group and -a

## Ad Hoc examples:
```
//TO INSTALL ON ALL NODES IN GROUP
ansible <group> -a/(FOR MODULE_ARGS/IM WRITING ARG AFTER THIS) "<linux command>"
ansible demoByYash -a "mkdir xyz"
//TO CREATE IN ALL NODES
ansible all -a "touch abcd"
//TO LIST ONLY IN LAST NODE
ansible demoByYash[0] -a "ls"
//TO INSTALL ON NODES RANGED
ansible demoByYash[0:3] -a "sudo apt install httpd" 
//TO NOT WRITE SUDO REPEATEDLY
ansible demoByYash -ba "apt install xyz"
```
If you run any of these 2wice, overwrite happens :( - imagine you started making changing to the abcd text file and saved it - when you run touch abcd again, existing file is overwritten with new file that has no content

## Ansible Modules
- Resources: predefined/readymade oneliner commands - when we install ansible these modules come with it 
- You can run these individually or collectively as playbook 
- Your library of module can be in any machine & no servers, daemons, db required
- def location of ansible modules: /etc/ansible/hosts
- IF SAME MODULE RUN AGAIN, YOU GET ALREADY INSTALLED!

## Sample Modules
```
By default, if a pkg is mentioned it means its being installed. But to specify the yaml,
Install = present
`ansible demoByYash -b -m apt -a "pkg=chessx state=present"`

Uninstall = absent
`ansible demoByYash -b -m apt -a "pkg=chessx state=absent"`

Update = latest
`ansible demoByYash -b -m apt -a "pkg=chessx state=update"`

Start = started
`ansible demoByYash -b -m apt -a "pkg=chessx state=started"`
```

- **ansible <group name> -b/sudo -m/module-name <name> "yaml command"**
- **apt module install**: The module name to be written after "-m" flag - in ad hocs, we dont put -a for argument w/o modules & "" dont have module. `ansible demoByYash -b -m apt -a "pkg=chessx state=present"`, ansible user only works with sudo/-b 
- **debian module update**: -m xyz is the module name and afterwards in "" we enter the yaml module. `Ex: ansible demoByYash -b -m apt -a "pkg = httpd state=update"`
- **service module start**: `Ex: ansible demoByYash -b -m service -a "name=httpd state=started"` 
- **user module create** To create a user we need not mentioned state=present but to delete, we use state=absent. `Ex: ansible demoByYash -b -m user -a "name-raj"`
- **copy module copying**: `Ex: ansible demoByYash -b -m copy -a "src=filekapath dest=/sourcekahanadalna` - every node in the group would have this file copied
- **ping module**: The “ping” module is used to verify the ability to manage remote nodes. `Ex: ansible all -m ping` 
- **command module**: When we run normal ad hoc commands w/o module name,
- VERY IMPORT **command module** selected by default. `Ex: ansible demoByYash -a "ls" = ansible demoByYash -m command -a "ls"` - it doesn't allow special characters like | for multi args - use **shell module** to bypass this `Ex:ansible demoByYash -m shell -a "ls | grep snap"`
- Some arguments are only available under a specific umbrella 

## Modules Examples
- Installing using apt module: `Ansible demoByYash -b -m apt -a "pkg=chessx state=present"` & ran `which chessx` on each node
```
192.168.122.128 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "cache_update_time": 1701320377,
    "cache_updated": false,
    "changed": true,
    "stderr": "",
    "stderr_lines": [],
    "stdout": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nThe following NEW packages will be installed:\n  chessx\n0 upgraded, 1 newly installed, 0 to remove and 63 not upgraded.\nNeed to get 0 B/3955 kB of archives.\nAfter this operation, 6885 kB of additional disk space will be used.\nSelecting previously unselected package chessx.\r\n(Reading database ... \r(Reading database ... 5%\r(Reading database ... 10%\r(Reading database ... 15%\r(Reading database ... 20%\r(Reading database ... 25%\r(Reading database ... 30%\r(Reading database ... 35%\r(Reading database ... 40%\r(Reading database ... 45%\r(Reading database ... 50%\r(Reading database ... 55%\r(Reading database ... 60%\r(Reading database ... 65%\r(Reading database ... 70%\r(Reading database ... 75%\r(Reading database ... 80%\r(Reading database ... 85%\r(Reading database ... 90%\r(Reading database ... 95%\r(Reading database ... 100%\r(Reading database ... 327121 files and directories currently installed.)\r\nPreparing to unpack .../chessx_1.4.6-2build1_amd64.deb ...\r\nUnpacking chessx (1.4.6-2build1) ...\r\nSetting up chessx (1.4.6-2build1) ...\r\nProcessing triggers for desktop-file-utils (0.26-1ubuntu5) ...\r\nProcessing triggers for gnome-menus (3.36.0-1.1ubuntu1) ...\r\nProcessing triggers for man-db (2.11.2-1) ...\r\nProcessing triggers for mailcap (3.70+nmu1ubuntu1) ...\r\n",
    "stdout_lines": [
        "Reading package lists...",
        "Building dependency tree...",
        "Reading state information...",
        "The following NEW packages will be installed:",
        "  chessx",
        "0 upgraded, 1 newly installed, 0 to remove and 63 not upgraded.",
        "Need to get 0 B/3955 kB of archives.",
        "After this operation, 6885 kB of additional disk space will be used.",
        "Selecting previously unselected package chessx.",
        "(Reading database ... ",
        "(Reading database ... 5%",
        "(Reading database ... 10%",
        "(Reading database ... 15%",
        "(Reading database ... 20%",
        "(Reading database ... 25%",
        "(Reading database ... 30%",
        "(Reading database ... 35%",
        "(Reading database ... 40%",
        "(Reading database ... 45%",
        "(Reading database ... 50%",
        "(Reading database ... 55%",
        "(Reading database ... 60%",
        "(Reading database ... 65%",
        "(Reading database ... 70%",
        "(Reading database ... 75%",
        "(Reading database ... 80%",
        "(Reading database ... 85%",
        "(Reading database ... 90%",
        "(Reading database ... 95%",
        "(Reading database ... 100%",
        "(Reading database ... 327121 files and directories currently installed.)",
        "Preparing to unpack .../chessx_1.4.6-2build1_amd64.deb ...",
        "Unpacking chessx (1.4.6-2build1) ...",
        "Setting up chessx (1.4.6-2build1) ...",
        "Processing triggers for desktop-file-utils (0.26-1ubuntu5) ...",
        "Processing triggers for gnome-menus (3.36.0-1.1ubuntu1) ...",
        "Processing triggers for man-db (2.11.2-1) ...",
        "Processing triggers for mailcap (3.70+nmu1ubuntu1) ..."
    ]
}
192.168.122.46 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "cache_update_time": 1701318415,
    "cache_updated": false,
    "changed": true,
    "stderr": "",
    "stderr_lines": [],
    "stdout": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nThe following NEW packages will be installed:\n  chessx\n0 upgraded, 1 newly installed, 0 to remove and 68 not upgraded.\nNeed to get 3955 kB of archives.\nAfter this operation, 6885 kB of additional disk space will be used.\nGet:1 http://in.archive.ubuntu.com/ubuntu lunar/universe amd64 chessx amd64 1.4.6-2build1 [3955 kB]\nFetched 3955 kB in 7s (608 kB/s)\nSelecting previously unselected package chessx.\r\n(Reading database ... \r(Reading database ... 5%\r(Reading database ... 10%\r(Reading database ... 15%\r(Reading database ... 20%\r(Reading database ... 25%\r(Reading database ... 30%\r(Reading database ... 35%\r(Reading database ... 40%\r(Reading database ... 45%\r(Reading database ... 50%\r(Reading database ... 55%\r(Reading database ... 60%\r(Reading database ... 65%\r(Reading database ... 70%\r(Reading database ... 75%\r(Reading database ... 80%\r(Reading database ... 85%\r(Reading database ... 90%\r(Reading database ... 95%\r(Reading database ... 100%\r(Reading database ... 327121 files and directories currently installed.)\r\nPreparing to unpack .../chessx_1.4.6-2build1_amd64.deb ...\r\nUnpacking chessx (1.4.6-2build1) ...\r\nSetting up chessx (1.4.6-2build1) ...\r\nProcessing triggers for desktop-file-utils (0.26-1ubuntu5) ...\r\nProcessing triggers for gnome-menus (3.36.0-1.1ubuntu1) ...\r\nProcessing triggers for man-db (2.11.2-1) ...\r\nProcessing triggers for mailcap (3.70+nmu1ubuntu1) ...\r\n",
    "stdout_lines": [
        "Reading package lists...",
        "Building dependency tree...",
        "Reading state information...",
        "The following NEW packages will be installed:",
        "  chessx",
        "0 upgraded, 1 newly installed, 0 to remove and 68 not upgraded.",
        "Need to get 3955 kB of archives.",
        "After this operation, 6885 kB of additional disk space will be used.",
        "Get:1 http://in.archive.ubuntu.com/ubuntu lunar/universe amd64 chessx amd64 1.4.6-2build1 [3955 kB]",
        "Fetched 3955 kB in 7s (608 kB/s)",
        "Selecting previously unselected package chessx.",
        "(Reading database ... ",
        "(Reading database ... 5%",
        "(Reading database ... 10%",
        "(Reading database ... 15%",
        "(Reading database ... 20%",
        "(Reading database ... 25%",
        "(Reading database ... 30%",
        "(Reading database ... 35%",
        "(Reading database ... 40%",
        "(Reading database ... 45%",
        "(Reading database ... 50%",
        "(Reading database ... 55%",
        "(Reading database ... 60%",
        "(Reading database ... 65%",
        "(Reading database ... 70%",
        "(Reading database ... 75%",
        "(Reading database ... 80%",
        "(Reading database ... 85%",
        "(Reading database ... 90%",
        "(Reading database ... 95%",
        "(Reading database ... 100%",
        "(Reading database ... 327121 files and directories currently installed.)",
        "Preparing to unpack .../chessx_1.4.6-2build1_amd64.deb ...",
        "Unpacking chessx (1.4.6-2build1) ...",
        "Setting up chessx (1.4.6-2build1) ...",
        "Processing triggers for desktop-file-utils (0.26-1ubuntu5) ...",
        "Processing triggers for gnome-menus (3.36.0-1.1ubuntu1) ...",
        "Processing triggers for man-db (2.11.2-1) ...",
        "Processing triggers for mailcap (3.70+nmu1ubuntu1) ..."
    ]
}

```
- Rerunning above module gives output of `already installed` - has idempotency 
```
192.168.122.128 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "cache_update_time": 1701320377,
    "cache_updated": false,
    "changed": false
}
192.168.122.46 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "cache_update_time": 1701318415,
    "cache_updated": false,
    "changed": false
}

```
- Updating using apt module: `ansible demoByYash -b -m apt -a "pkg=chessx state=latest"`
Output:
```
192.168.122.128 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "cache_update_time": 1701320377,
    "cache_updated": false,
    "changed": false
}
192.168.122.46 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "cache_update_time": 1701318415,
    "cache_updated": false,
    "changed": false
}
```

- Using service modules
- - Stopping service using service module using
`ansible demoByYash -m service -a "name=chessx service=stopped"`
```
[WARNING]: Both option name and its alias service are set.
192.168.122.46 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "name": "stopped",
    "status": {
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "inactive",
        "AllowIsolate": "no",
        "AssertResult": "no",
        "AssertTimestampMonotonic": "0",
        "BlockIOAccounting": "no",
        "BlockIOWeight": "[not set]",
        "CPUAccounting": "yes",
        "CPUAffinityFromNUMA": "no",
        "CPUQuotaPerSecUSec": "infinity",
        "CPUQuotaPeriodUSec": "infinity",
        "CPUSchedulingPolicy": "0",
        "CPUSchedulingPriority": "0",
        "CPUSchedulingResetOnFork": "no",
        "CPUShares": "[not set]",
        "CPUUsageNSec": "[not set]",
        "CPUWeight": "[not set]",
        "CacheDirectoryMode": "0755",
        "CanFreeze": "yes",
        "CanIsolate": "no",
        "CanReload": "no",
        "CanStart": "no",
        "CanStop": "yes",
        "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon cap_bpf cap_checkpoint_restore",
        "CleanResult": "success",
        "CollectMode": "inactive",
        "ConditionResult": "no",
        "ConditionTimestampMonotonic": "0",
        "ConfigurationDirectoryMode": "0755",
        "ControlGroupId": "0",
        "ControlPID": "0",
        "CoredumpFilter": "0x33",
        "DefaultDependencies": "yes",
        "DefaultMemoryLow": "0",
        "DefaultMemoryMin": "0",
        "Delegate": "no",
        "Description": "stopped.service",
        "DevicePolicy": "auto",
        "DynamicUser": "no",
        "ExecMainCode": "0",
        "ExecMainExitTimestampMonotonic": "0",
        "ExecMainPID": "0",
        "ExecMainStartTimestampMonotonic": "0",
        "ExecMainStatus": "0",
        "ExitType": "main",
        "FailureAction": "none",
        "FileDescriptorStoreMax": "0",
        "FinalKillSignal": "9",
        "FreezerState": "running",
        "GID": "[not set]",
        "GuessMainPID": "yes",
        "IOAccounting": "no",
        "IOReadBytes": "18446744073709551615",
        "IOReadOperations": "18446744073709551615",
        "IOSchedulingClass": "2",
        "IOSchedulingPriority": "4",
        "IOWeight": "[not set]",
        "IOWriteBytes": "18446744073709551615",
        "IOWriteOperations": "18446744073709551615",
        "IPAccounting": "no",
        "IPEgressBytes": "[no data]",
        "IPEgressPackets": "[no data]",
        "IPIngressBytes": "[no data]",
        "IPIngressPackets": "[no data]",
        "Id": "stopped.service",
        "IgnoreOnIsolate": "no",
        "IgnoreSIGPIPE": "yes",
        "InactiveEnterTimestampMonotonic": "0",
        "InactiveExitTimestampMonotonic": "0",
        "JobRunningTimeoutUSec": "infinity",
        "JobTimeoutAction": "none",
        "JobTimeoutUSec": "infinity",
        "KeyringMode": "private",
        "KillMode": "control-group",
        "KillSignal": "15",
        "LimitAS": "infinity",
        "LimitASSoft": "infinity",
        "LimitCORE": "infinity",
        "LimitCORESoft": "0",
        "LimitCPU": "infinity",
        "LimitCPUSoft": "infinity",
        "LimitDATA": "infinity",
        "LimitDATASoft": "infinity",
        "LimitFSIZE": "infinity",
        "LimitFSIZESoft": "infinity",
        "LimitLOCKS": "infinity",
        "LimitLOCKSSoft": "infinity",
        "LimitMEMLOCK": "512135168",
        "LimitMEMLOCKSoft": "512135168",
        "LimitMSGQUEUE": "819200",
        "LimitMSGQUEUESoft": "819200",
        "LimitNICE": "0",
        "LimitNICESoft": "0",
        "LimitNOFILE": "1048576",
        "LimitNOFILESoft": "1048576",
        "LimitNPROC": "15336",
        "LimitNPROCSoft": "15336",
        "LimitRSS": "infinity",
        "LimitRSSSoft": "infinity",
        "LimitRTPRIO": "0",
        "LimitRTPRIOSoft": "0",
        "LimitRTTIME": "infinity",
        "LimitRTTIMESoft": "infinity",
        "LimitSIGPENDING": "15336",
        "LimitSIGPENDINGSoft": "15336",
        "LimitSTACK": "infinity",
        "LimitSTACKSoft": "8388608",
        "LoadError": "org.freedesktop.systemd1.NoSuchUnit \"Unit stopped.service not found.\"",
        "LoadState": "not-found",
        "LockPersonality": "no",
        "LogLevelMax": "-1",
        "LogRateLimitBurst": "0",
        "LogRateLimitIntervalUSec": "0",
        "LogsDirectoryMode": "0755",
        "MainPID": "0",
        "ManagedOOMMemoryPressure": "auto",
        "ManagedOOMMemoryPressureLimit": "0",
        "ManagedOOMPreference": "none",
        "ManagedOOMSwap": "auto",
        "MemoryAccounting": "yes",
        "MemoryAvailable": "infinity",
        "MemoryCurrent": "[not set]",
        "MemoryDenyWriteExecute": "no",
        "MemoryHigh": "infinity",
        "MemoryLimit": "infinity",
        "MemoryLow": "0",
        "MemoryMax": "infinity",
        "MemoryMin": "0",
        "MemorySwapMax": "infinity",
        "MountAPIVFS": "no",
        "NFileDescriptorStore": "0",
        "NRestarts": "0",
        "NUMAPolicy": "n/a",
        "Names": "stopped.service",
        "NeedDaemonReload": "no",
        "Nice": "0",
        "NoNewPrivileges": "no",
        "NonBlocking": "no",
        "NotifyAccess": "none",
        "OOMScoreAdjust": "0",
        "OnFailureJobMode": "replace",
        "OnSuccessJobMode": "fail",
        "Perpetual": "no",
        "PrivateDevices": "no",
        "PrivateIPC": "no",
        "PrivateMounts": "no",
        "PrivateNetwork": "no",
        "PrivateTmp": "no",
        "PrivateUsers": "no",
        "ProcSubset": "all",
        "ProtectClock": "no",
        "ProtectControlGroups": "no",
        "ProtectHome": "no",
        "ProtectHostname": "no",
        "ProtectKernelLogs": "no",
        "ProtectKernelModules": "no",
        "ProtectKernelTunables": "no",
        "ProtectProc": ansible demoByYash -m service -a "name=chessx service=stopped"[WARNING]: Both option name and its alias service are set.
192.168.122.46 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "name": "stopped",
    "status": {
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "inactive",
        "AllowIsolate": "no",
        "AssertResult": "no",
        "AssertTimestampMonotonic": "0",
        "BlockIOAccounting": "no",
        "BlockIOWeight": "[not set]",
        "CPUAccounting": "yes",
        "CPUAffinityFromNUMA": "no",
        "CPUQuotaPerSecUSec": "infinity",
        "CPUQuotaPeriodUSec": "infinity",
        "CPUSchedulingPolicy": "0",
        "CPUSchedulingPriority": "0",
        "CPUSchedulingResetOnFork": "no",
        "CPUShares": "[not set]",
        "CPUUsageNSec": "[not set]",
        "CPUWeight": "[not set]",
        "CacheDirectoryMode": "0755",
        "CanFreeze": "yes",
        "CanIsolate": "no",
        "CanReload": "no",
        "CanStart": "no",
        "CanStop": "yes",
        "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon cap_bpf cap_checkpoint_restore",
        "CleanResult": "success",
        "CollectMode": "inactive",
        "ConditionResult": "no",
        "ConditionTimestampMonotonic": "0",
        "ConfigurationDirectoryMode": "0755",
        "ControlGroupId": "0",
        "ControlPID": "0",
        "CoredumpFilter": "0x33",
        "DefaultDependencies": "yes",
        "DefaultMemoryLow": "0",
        "DefaultMemoryMin": "0",
        "Delegate": "no",
        "Description": "stopped.service",
        "DevicePolicy": "auto",
        "DynamicUser": "no",
        "ExecMainCode": "0",
        "ExecMainExitTimestampMonotonic": "0",
        "ExecMainPID": "0",
        "ExecMainStartTimestampMonotonic": "0",
        "ExecMainStatus": "0",
        "ExitType": "main",
        "FailureAction": "none",
        "FileDescriptorStoreMax": "0",
        "FinalKillSignal": "9",
        "FreezerState": "running",
        "GID": "[not set]",
        "GuessMainPID": "yes",
        "IOAccounting": "no",
        "IOReadBytes": "18446744073709551615",
        "IOReadOperations": "18446744073709551615",
        "IOSchedulingClass": "2",
        "IOSchedulingPriority": "4",
        "IOWeight": "[not set]",
        "IOWriteBytes": "18446744073709551615",
        "IOWriteOperations": "18446744073709551615",
        "IPAccounting": "no",
        "IPEgressBytes": "[no data]",
        "IPEgressPackets": "[no data]",
        "IPIngressBytes": "[no data]",
        "IPIngressPackets": "[no data]",
        "Id": "stopped.service",
        "IgnoreOnIsolate": "no",
        "IgnoreSIGPIPE": "yes",
        "InactiveEnterTimestampMonotonic": "0",
        "InactiveExitTimestampMonotonic": "0",
        "JobRunningTimeoutUSec": "infinity",
        "JobTimeoutAction": "none",
        "JobTimeoutUSec": "infinity",
        "KeyringMode": "private",
        "KillMode": "control-group",
        "KillSignal": "15",
        "LimitAS": "infinity",
        "LimitASSoft": "infinity",
        "LimitCORE": "infinity",
        "LimitCORESoft": "0",
        "LimitCPU": "infinity",
        "LimitCPUSoft": "infinity",
        "LimitDATA": "infinity",
        "LimitDATASoft": "infinity",
        "LimitFSIZE": "infinity",
        "LimitFSIZESoft": "infinity",
        "LimitLOCKS": "infinity",
        "LimitLOCKSSoft": "infinity",
        "LimitMEMLOCK": "512135168",
        "LimitMEMLOCKSoft": "512135168",
        "LimitMSGQUEUE": "819200",
        "LimitMSGQUEUESoft": "819200",
        "LimitNICE": "0",
        "LimitNICESoft": "0",
        "LimitNOFILE": "1048576",
        "LimitNOFILESoft": "1048576",
        "LimitNPROC": "15336",
        "LimitNPROCSoft": "15336",
        "LimitRSS": "infinity",
        "LimitRSSSoft": "infinity",
        "LimitRTPRIO": "0",
        "LimitRTPRIOSoft": "0",
        "LimitRTTIME": "infinity",
        "LimitRTTIMESoft": "infinity",
        "LimitSIGPENDING": "15336",
        "LimitSIGPENDINGSoft": "15336",
        "LimitSTACK": "infinity",
        "LimitSTACKSoft": "8388608",
        "LoadError": "org.freedesktop.systemd1.NoSuchUnit \"Unit stopped.service not found.\"",
        "LoadState": "not-found",
        "LockPersonality": "no",
        "LogLevelMax": "-1",
        "LogRateLimitBurst": "0",
        "LogRateLimitIntervalUSec": "0",
        "LogsDirectoryMode": "0755",
        "MainPID": "0",
        "ManagedOOMMemoryPressure": "auto",
        "ManagedOOMMemoryPressureLimit": "0",
        "ManagedOOMPreference": "none",
        "ManagedOOMSwap": "auto",
        "MemoryAccounting": "yes",
        "MemoryAvailable": "infinity",
        "MemoryCurrent": "[not set]",
        "MemoryDenyWriteExecute": "no",
        "MemoryHigh": "infinity",
        "MemoryLimit": "infinity",
        "MemoryLow": "0",
        "MemoryMax": "infinity",
        "MemoryMin": "0",
        "MemorySwapMax": "infinity",
        "MountAPIVFS": "no",
        "NFileDescriptorStore": "0",
        "NRestarts": "0",
        "NUMAPolicy": "n/a",
        "Names": "stopped.service",
        "NeedDaemonReload": "no",
        "Nice": "0",
        "NoNewPrivileges": "no",
        "NonBlocking": "no",
        "NotifyAccess": "none",
        "OOMScoreAdjust": "0",
        "OnFailureJobMode": "replace",
        "OnSuccessJobMode": "fail",
        "Perpetual": "no",
        "PrivateDevices": "no",
        "PrivateIPC": "no",
        "PrivateMounts": "no",
        "PrivateNetwork": "no",
        "PrivateTmp": "no",
        "PrivateUsers": "no",
        "ProcSubset": "all",
        "ProtectClock": "no",
        "ProtectControlGroups": "no",
        "ProtectHome": "no",
        "ProtectHostname": "no",
        "ProtectKernelLogs": "no",
        "ProtectKernelModules": "no",
        "ProtectKernelTunables": "no",
        "ProtectProc": "default",
        "ProtectSystem": "no",
        "RefuseManualStart": "no",
        "RefuseManualStop": "no",
        "ReloadResult": "success",
        "RemainAfterExit": "no",
        "RemoveIPC": "no",
        "Restart": "no",
        "RestartKillSignal": "15",
        "RestartUSec": "100ms",
        "RestrictNamespaces": "no",
        "RestrictRealtime": "no",
        "RestrictSUIDSGID": "no",
        "Result": "success",
        "RootDirectoryStartOnly": "no",
        "RuntimeDirectoryMode": "0755",
        "RuntimeDirectoryPreserve": "no",
        "RuntimeMaxUSec": "infinity",
        "RuntimeRandomizedExtraUSec": "0",
        "SameProcessGroup": "no",
        "SecureBits": "0",
        "SendSIGHUP": "no",
        "SendSIGKILL": "yes",
        "StandardError": "inherit",
        "StandardInput": "null",
        "StandardOutput": "inherit",
        "StartLimitAction": "none",
        "StartLimitBurst": "5",
        "StartLimitIntervalUSec": "10s",
        "StartupBlockIOWeight": "[not set]",
        "StartupCPUShares": "[not set]",
        "StartupCPUWeight": "[not set]",
        "StartupIOWeight": "[not set]",
        "StateChangeTimestampMonotonic": "0",
        "StateDirectoryMode": "0755",
        "StatusErrno": "0",
        "StopWhenUnneeded": "no",
        "SubState": "dead",
        "SuccessAction": "none",
        "SyslogFacility": "3",
        "SyslogLevel": "6",
        "SyslogLevelPrefix": "yes",
        "SyslogPriority": "30",
        "SystemCallErrorNumber": "2147483646",
        "TTYReset": "no",
        "TTYVHangup": "no",
        "TTYVTDisallocate": "no",
        "TasksAccounting": "yes",
        "TasksCurrent": "[not set]",
        "TasksMax": "4600",
        "TimeoutAbortUSec": "1min 30s",
        "TimeoutCleanUSec": "infinity",
        "TimeoutStartFailureMode": "terminate",
        "TimeoutStartUSec": "1min 30s",
        "TimeoutStopFailureMode": "terminate",
        "TimeoutStopUSec": "1min 30s",
        "TimerSlackNSec": "50000",
        "Transient": "no",
        "UID": "[not set]",
        "UMask": "0022",
        "UtmpMode": "init",
        "WatchdogSignal": "6",
        "WatchdogTimestampMonotonic": "0",
        "WatchdogUSec": "infinity"
    }
}
192.168.122.128 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "name": "stopped",
    "status": {
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "inactive",
        "AllowIsolate": "no",
        "AssertResult": "no",
        "AssertTimestampMonotonic": "0",
        "BlockIOAccounting": "no",
        "BlockIOWeight": "[not set]",
        "CPUAccounting": "yes",
        "CPUAffinityFromNUMA": "no",
        "CPUQuotaPerSecUSec": "infinity",
        "CPUQuotaPeriodUSec": "infinity",
        "CPUSchedulingPolicy": "0",
        "CPUSchedulingPriority": "0",
        "CPUSchedulingResetOnFork": "no",
        "CPUShares": "[not set]",
        "CPUUsageNSec": "[not set]",
        "CPUWeight": "[not set]",
        "CacheDirectoryMode": "0755",
        "CanFreeze": "yes",
        "CanIsolate": "no",
        "CanReload": "no",
        "CanStart": "no",
        "CanStop": "yes",
        "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon cap_bpf cap_checkpoint_restore",
        "CleanResult": "success",
        "CollectMode": "inactive",
        "ConditionResult": "no",
        "ConditionTimestampMonotonic": "0",
        "ConfigurationDirectoryMode": "0755",
        "ControlGroupId": "0",
        "ControlPID": "0",
        "CoredumpFilter": "0x33",
        "DefaultDependencies": "yes",
        "DefaultMemoryLow": "0",
        "DefaultMemoryMin": "0",
        "Delegate": "no",
        "Description": "stopped.service",
        "DevicePolicy": "auto",
        "DynamicUser": "no",
        "ExecMainCode": "0",
        "ExecMainExitTimestampMonotonic": "0",
        "ExecMainPID": "0",
        "ExecMainStartTimestampMonotonic": "0",
        "ExecMainStatus": "0",
        "ExitType": "main",
        "FailureAction": "none",
        "FileDescriptorStoreMax": "0",
        "FinalKillSignal": "9",
        "FreezerState": "running",
        "GID": "[not set]",
        "GuessMainPID": "yes",
        "IOAccounting": "no",
        "IOReadBytes": "18446744073709551615",
        "IOReadOperations": "18446744073709551615",
        "IOSchedulingClass": "2",
        "IOSchedulingPriority": "4",
        "IOWeight": "[not set]",
        "IOWriteBytes": "18446744073709551615",
        "IOWriteOperations": "18446744073709551615",
        "IPAccounting": "no",
        "IPEgressBytes": "[no data]",
        "IPEgressPackets": "[no data]",
        "IPIngressBytes": "[no data]",
        "IPIngressPackets": "[no data]",
        "Id": "stopped.service",
        "IgnoreOnIsolate": "no",
        "IgnoreSIGPIPE": "yes",
        "InactiveEnterTimestampMonotonic": "0",
        "InactiveExitTimestampMonotonic": "0",
        "JobRunningTimeoutUSec": "infinity",
        "JobTimeoutAction": "none",
        "JobTimeoutUSec": "infinity",
        "KeyringMode": "private",
        "KillMode": "control-group",
        "KillSignal": "15",
        "LimitAS": "infinity",
        "LimitASSoft": "infinity",
        "LimitCORE": "infinity",
        "LimitCORESoft": "0",
        "LimitCPU": "infinity",
        "LimitCPUSoft": "infinity",
        "LimitDATA": "infinity",
        "LimitDATASoft": "infinity",
        "LimitFSIZE": "infinity",
        "LimitFSIZESoft": "infinity",
        "LimitLOCKS": "infinity",
        "LimitLOCKSSoft": "infinity",
        "LimitMEMLOCK": "512135168",
        "LimitMEMLOCKSoft": "512135168",
        "LimitMSGQUEUE": "819200",
        "LimitMSGQUEUESoft": "819200",
        "LimitNICE": "0",
        "LimitNICESoft": "0",
        "LimitNOFILE": "1048576",
        "LimitNOFILESoft": "1048576",
        "LimitNPROC": "15336",
        "LimitNPROCSoft": "15336",
        "LimitRSS": "infinity",
        "LimitRSSSoft": "infinity",
        "LimitRTPRIO": "0",
        "LimitRTPRIOSoft": "0",
        "LimitRTTIME": "infinity",
        "LimitRTTIMESoft": "infinity",
        "LimitSIGPENDING": "15336",
        "LimitSIGPENDINGSoft": "15336",
        "LimitSTACK": "infinity",
        "LimitSTACKSoft": "8388608",
        "LoadError": "org.freedesktop.systemd1.NoSuchUnit \"Unit stopped.service not found.\"",
        "LoadState": "not-found",
        "LockPersonality": "no",
        "LogLevelMax": "-1",
        "LogRateLimitBurst": "0",
        "LogRateLimitIntervalUSec": "0",
        "LogsDirectoryMode": "0755",
        "MainPID": "0",
        "ManagedOOMMemoryPressure": "auto",
        "ManagedOOMMemoryPressureLimit": "0",
        "ManagedOOMPreference": "none",
        "ManagedOOMSwap": "auto",
        "MemoryAccounting": "yes",
        "MemoryAvailable": "infinity",
        "MemoryCurrent": "[not set]",
        "MemoryDenyWriteExecute": "no",
        "MemoryHigh": "infinity",
        "MemoryLimit": "infinity",
        "MemoryLow": "0",
        "MemoryMax": "infinity",
        "MemoryMin": "0",
        "MemorySwapMax": "infinity",
        "MountAPIVFS": "no",
        "NFileDescriptorStore": "0",
        "NRestarts": "0",
        "NUMAPolicy": "n/a",
        "Names": "stopped.service",
        "NeedDaemonReload": "no",
        "Nice": "0",
        "NoNewPrivileges": "no",
        "NonBlocking": "no",
        "NotifyAccess": "none",
        "OOMScoreAdjust": "0",
        "OnFailureJobMode": "replace",
        "OnSuccessJobMode": "fail",
        "Perpetual": "no",
        "PrivateDevices": "no",
        "PrivateIPC": "no",
        "PrivateMounts": "no",
        "PrivateNetwork": "no",
        "PrivateTmp": "no",
        "PrivateUsers": "no",
        "ProcSubset": "all",
        "ProtectClock": "no",
        "ProtectControlGroups": "no",
        "ProtectHome": "no",
        "ProtectHostname": "no",
        "ProtectKernelLogs": "no",
        "ProtectKernelModules": "no",
        "ProtectKernelTunables": "no",
        "ProtectProc": "default",
        "ProtectSystem": "no",
        "RefuseManualStart": "no",
        "RefuseManualStop": "no",
        "ReloadResult": "success",
        "RemainAfterExit": "no",
        "RemoveIPC": "no",
        "Restart": "no",
        "RestartKillSignal": "15",
        "RestartUSec": "100ms",
        "RestrictNamespaces": "no",
        "RestrictRealtime": "no",
        "RestrictSUIDSGID": "no",
        "Result": "success",
        "RootDirectoryStartOnly": "no",
        "RuntimeDirectoryMode": "0755",
        "RuntimeDirectoryPreserve": "no",
        "RuntimeMaxUSec": "infinity",
        "RuntimeRandomizedExtraUSec": "0",
        "SameProcessGroup": "no",
        "SecureBits": "0",
        "SendSIGHUP": "no",
        "SendSIGKILL": "yes",
        "StandardError": "inherit",
        "StandardInput": "null",
        "StandardOutput": "inherit",
        "StartLimitAction": "none",
        "StartLimitBurst": "5",
        "StartLimitIntervalUSec": "10s",
        "StartupBlockIOWeight": "[not set]",
        "StartupCPUShares": "[not set]",
        "StartupCPUWeight": "[not set]",
        "StartupIOWeight": "[not set]",
        "StateChangeTimestampMonotonic": "0",
        "StateDirectoryMode": "0755",
        "StatusErrno": "0",
        "StopWhenUnneeded": "no",
        "SubState": "dead",
        "SuccessAction": "none",
        "SyslogFacility": "3",
        "SyslogLevel": "6",
        "SyslogLevelPrefix": "yes",
        "SyslogPriority": "30",
        "SystemCallErrorNumber": "2147483646",
        "TTYReset": "no",
        "TTYVHangup": "no",
        "TTYVTDisallocate": "no",
        "TasksAccounting": "yes",
        "TasksCurrent": "[not set]",
        "TasksMax": "4600",
        "TimeoutAbortUSec": "1min 30s",
        "TimeoutCleanUSec": "infinity",
        "TimeoutStartFailureMode": "terminate",
        "TimeoutStartUSec": "1min 30s",
        "TimeoutStopFailureMode": "terminate",
        "TimeoutStopUSec": "1min 30s",
        "TimerSlackNSec": "50000",
        "Transient": "no",
        "UID": "[not set]",
        "UMask": "0022",
        "UtmpMode": "init",
        "WatchdogSignal": "6",
        "WatchdogTimestampMonotonic": "0",
        "WatchdogUSec": "infinity"
    }
}
"default",
        "ProtectSystem": "no",
        "RefuseManualStart": "no",
        "RefuseManualStop": "no",
        "ReloadResult": "success",
        "RemainAfterExit": "no",
        "RemoveIPC": "no",
        "Restart": "no",
        "RestartKillSignal": "15",
        "RestartUSec": "100ms",
        "RestrictNamespaces": "no",
        "RestrictRealtime": "no",
        "RestrictSUIDSGID": "no",
        "Result": "success",
        "RootDirectoryStartOnly": "no",
        "RuntimeDirectoryMode": "0755",
        "RuntimeDirectoryPreserve": "no",
        "RuntimeMaxUSec": "infinity",
        "RuntimeRandomizedExtraUSec": "0",
        "SameProcessGroup": "no",
        "SecureBits": "0",
        "SendSIGHUP": "no",
        "SendSIGKILL": "yes",
        "StandardError": "inherit",
        "StandardInput": "null",
        "StandardOutput": "inherit",
        "StartLimitAction": "none",
        "StartLimitBurst": "5",
        "StartLimitIntervalUSec": "10s",
        "StartupBlockIOWeight": "[not set]",
        "StartupCPUShares": "[not set]",
        "StartupCPUWeight": "[not set]",
        "StartupIOWeight": "[not set]",
        "StateChangeTimestampMonotonic": "0",
        "StateDirectoryMode": "0755",
        "StatusErrno": "0",
        "StopWhenUnneeded": "no",
        "SubState": "dead",
        "SuccessAction": "none",
        "SyslogFacility": "3",
        "SyslogLevel": "6",
        "SyslogLevelPrefix": "yes",
        "SyslogPriority": "30",
        "SystemCallErrorNumber": "2147483646",
        "TTYReset": "no",
        "TTYVHangup": "no",
        "TTYVTDisallocate": "no",
        "TasksAccounting": "yes",
        "TasksCurrent": "[not set]",
        "TasksMax": "4600",
        "TimeoutAbortUSec": "1min 30s",
        "TimeoutCleanUSec": "infinity",
        "TimeoutStartFailureMode": "terminate",
        "TimeoutStartUSec": "1min 30s",
        "TimeoutStopFailureMode": "terminate",
        "TimeoutStopUSec": "1min 30s",
        "TimerSlackNSec": "50000",
        "Transient": "no",
        "UID": "[not set]",
        "UMask": "0022",
        "UtmpMode": "init",
        "WatchdogSignal": "6",
        "WatchdogTimestampMonotonic": "0",
        "WatchdogUSec": "infinity"
    }
}
192.168.122.128 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "name": "stopped",
    "status": {
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "inactive",
        "AllowIsolate": "no",
        "AssertResult": "no",
        "AssertTimestampMonotonic": "0",
        "BlockIOAccounting": "no",
        "BlockIOWeight": "[not set]",
        "CPUAccounting": "yes",
        "CPUAffinityFromNUMA": "no",
        "CPUQuotaPerSecUSec": "infinity",
        "CPUQuotaPeriodUSec": "infinity",
        "CPUSchedulingPolicy": "0",
        "CPUSchedulingPriority": "0",
        "CPUSchedulingResetOnFork": "no",
        "CPUShares": "[not set]",
        "CPUUsageNSec": "[not set]",
        "CPUWeight": "[not set]",
        "CacheDirectoryMode": "0755",
        "CanFreeze": "yes",
        "CanIsolate": "no",
        "CanReload": "no",
        "CanStart": "no",
        "CanStop": "yes",
        "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon cap_bpf cap_checkpoint_restore",
        "CleanResult": "success",
        "CollectMode": "inactive",
        "ConditionResult": "no",
        "ConditionTimestampMonotonic": "0",
        "ConfigurationDirectoryMode": "0755",
        "ControlGroupId": "0",
        "ControlPID": "0",
        "CoredumpFilter": "0x33",
        "DefaultDependencies": "yes",
        "DefaultMemoryLow": "0",
        "DefaultMemoryMin": "0",
        "Delegate": "no",
        "Description": "stopped.service",
        "DevicePolicy": "auto",
        "DynamicUser": "no",
        "ExecMainCode": "0",
        "ExecMainExitTimestampMonotonic": "0",
        "ExecMainPID": "0",
        "ExecMainStartTimestampMonotonic": "0",
        "ExecMainStatus": "0",
        "ExitType": "main",
        "FailureAction": "none",
        "FileDescriptorStoreMax": "0",
        "FinalKillSignal": "9",
        "FreezerState": "running",
        "GID": "[not set]",
        "GuessMainPID": "yes",
        "IOAccounting": "no",
        "IOReadBytes": "18446744073709551615",
        "IOReadOperations": "18446744073709551615",
        "IOSchedulingClass": "2",
        "IOSchedulingPriority": "4",
        "IOWeight": "[not set]",
        "IOWriteBytes": "18446744073709551615",
        "IOWriteOperations": "18446744073709551615",
        "IPAccounting": "no",
        "IPEgressBytes": "[no data]",
        "IPEgressPackets": "[no data]",
        "IPIngressBytes": "[no data]",
        "IPIngressPackets": "[no data]",
        "Id": "stopped.service",
        "IgnoreOnIsolate": "no",
        "IgnoreSIGPIPE": "yes",
        "InactiveEnterTimestampMonotonic": "0",
        "InactiveExitTimestampMonotonic": "0",
        "JobRunningTimeoutUSec": "infinity",
        "JobTimeoutAction": "none",
        "JobTimeoutUSec": "infinity",
        "KeyringMode": "private",
        "KillMode": "control-group",
        "KillSignal": "15",
        "LimitAS": "infinity",
        "LimitASSoft": "infinity",
        "LimitCORE": "infinity",
        "LimitCORESoft": "0",
        "LimitCPU": "infinity",
        "LimitCPUSoft": "infinity",
        "LimitDATA": "infinity",
        "LimitDATASoft": "infinity",
        "LimitFSIZE": "infinity",
        "LimitFSIZESoft": "infinity",
        "LimitLOCKS": "infinity",
        "LimitLOCKSSoft": "infinity",
        "LimitMEMLOCK": "512135168",
        "LimitMEMLOCKSoft": "512135168",
        "LimitMSGQUEUE": "819200",
        "LimitMSGQUEUESoft": "819200",
        "LimitNICE": "0",
        "LimitNICESoft": "0",
        "LimitNOFILE": "1048576",
        "LimitNOFILESoft": "1048576",
        "LimitNPROC": "15336",
        "LimitNPROCSoft": "15336",
        "LimitRSS": "infinity",
        "LimitRSSSoft": "infinity",
        "LimitRTPRIO": "0",
        "LimitRTPRIOSoft": "0",
        "LimitRTTIME": "infinity",
        "LimitRTTIMESoft": "infinity",
        "LimitSIGPENDING": "15336",
        "LimitSIGPENDINGSoft": "15336",
        "LimitSTACK": "infinity",
        "LimitSTACKSoft": "8388608",
        "LoadError": "org.freedesktop.systemd1.NoSuchUnit \"Unit stopped.service not found.\"",
        "LoadState": "not-found",
        "LockPersonality": "no",
        "LogLevelMax": "-1",
        "LogRateLimitBurst": "0",
        "LogRateLimitIntervalUSec": "0",
        "LogsDirectoryMode": "0755",
        "MainPID": "0",
        "ManagedOOMMemoryPressure": "auto",
        "ManagedOOMMemoryPressureLimit": "0",
        "ManagedOOMPreference": "none",
        "ManagedOOMSwap": "auto",
        "MemoryAccounting": "yes",
        "MemoryAvailable": "infinity",
        "MemoryCurrent": "[not set]",
        "MemoryDenyWriteExecute": "no",
        "MemoryHigh": "infinity",
        "MemoryLimit": "infinity",
        "MemoryLow": "0",
        "MemoryMax": "infinity",
        "MemoryMin": "0",
        "MemorySwapMax": "infinity",
        "MountAPIVFS": "no",
        "NFileDescriptorStore": "0",
        "NRestarts": "0",
        "NUMAPolicy": "n/a",
        "Names": "stopped.service",
        "NeedDaemonReload": "no",
        "Nice": "0",
        "NoNewPrivileges": "no",
        "NonBlocking": "no",
        "NotifyAccess": "none",
        "OOMScoreAdjust": "0",
        "OnFailureJobMode": "replace",
        "OnSuccessJobMode": "fail",
        "Perpetual": "no",
        "PrivateDevices": "no",
        "PrivateIPC": "no",
        "PrivateMounts": "no",
        "PrivateNetwork": "no",
        "PrivateTmp": "no",
        "PrivateUsers": "no",
        "ProcSubset": "all",
        "ProtectClock": "no",
        "ProtectControlGroups": "no",
        "ProtectHome": "no",
        "ProtectHostname": "no",
        "ProtectKernelLogs": "no",
        "ProtectKernelModules": "no",
        "ProtectKernelTunables": "no",
        "ProtectProc": "default",
        "ProtectSystem": "no",
        "RefuseManualStart": "no",
        "RefuseManualStop": "no",
        "ReloadResult": "success",
        "RemainAfterExit": "no",
        "RemoveIPC": "no",
        "Restart": "no",
        "RestartKillSignal": "15",
        "RestartUSec": "100ms",
        "RestrictNamespaces": "no",
        "RestrictRealtime": "no",
        "RestrictSUIDSGID": "no",
        "Result": "success",
        "RootDirectoryStartOnly": "no",
        "RuntimeDirectoryMode": "0755",
        "RuntimeDirectoryPreserve": "no",
        "RuntimeMaxUSec": "infinity",
        "RuntimeRandomizedExtraUSec": "0",
        "SameProcessGroup": "no",
        "SecureBits": "0",
        "SendSIGHUP": "no",
        "SendSIGKILL": "yes",
        "StandardError": "inherit",
        "StandardInput": "null",
        "StandardOutput": "inherit",
        "StartLimitAction": "none",
        "StartLimitBurst": "5",
        "StartLimitIntervalUSec": "10s",
        "StartupBlockIOWeight": "[not set]",
        "StartupCPUShares": "[not set]",
        "StartupCPUWeight": "[not set]",
        "StartupIOWeight": "[not set]",
        "StateChangeTimestampMonotonic": "0",
        "StateDirectoryMode": "0755",
        "StatusErrno": "0",
        "StopWhenUnneeded": "no",
        "SubState": "dead",
        "SuccessAction": "none",
        "SyslogFacility": "3",
        "SyslogLevel": "6",
        "SyslogLevelPrefix": "yes",
        "SyslogPriority": "30",
        "SystemCallErrorNumber": "2147483646",
        "TTYReset": "no",
        "TTYVHangup": "no",
        "TTYVTDisallocate": "no",
        "TasksAccounting": "yes",
        "TasksCurrent": "[not set]",
        "TasksMax": "4600",
        "TimeoutAbortUSec": "1min 30s",
        "TimeoutCleanUSec": "infinity",
        "TimeoutStartFailureMode": "terminate",
        "TimeoutStartUSec": "1min 30s",
        "TimeoutStopFailureMode": "terminate",
        "TimeoutStopUSec": "1min 30s",
        "TimerSlackNSec": "50000",
        "Transient": "no",
        "UID": "[not set]",
        "UMask": "0022",
        "UtmpMode": "init",
        "WatchdogSignal": "6",
        "WatchdogTimestampMonotonic": "0",
        "WatchdogUSec": "infinity"
    }
}
```

- - Starting service using service module using `ansible demoByYash -m service -a "name=chessx service=started"`
```
[WARNING]: Both option name and its alias service are set.
192.168.122.128 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "name": "started",
    "status": {
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "inactive",
        "AllowIsolate": "no",
        "AssertResult": "no",
        "AssertTimestampMonotonic": "0",
        "BlockIOAccounting": "no",
        "BlockIOWeight": "[not set]",
        "CPUAccounting": "yes",
        "CPUAffinityFromNUMA": "no",
        "CPUQuotaPerSecUSec": "infinity",
        "CPUQuotaPeriodUSec": "infinity",
        "CPUSchedulingPolicy": "0",
        "CPUSchedulingPriority": "0",
        "CPUSchedulingResetOnFork": "no",
        "CPUShares": "[not set]",
        "CPUUsageNSec": "[not set]",
        "CPUWeight": "[not set]",
        "CacheDirectoryMode": "0755",
        "CanFreeze": "yes",
        "CanIsolate": "no",
        "CanReload": "no",
        "CanStart": "no",
        "CanStop": "yes",
        "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon cap_bpf cap_checkpoint_restore",
        "CleanResult": "success",
        "CollectMode": "inactive",
        "ConditionResult": "no",
        "ConditionTimestampMonotonic": "0",
        "ConfigurationDirectoryMode": "0755",
        "ControlGroupId": "0",
        "ControlPID": "0",
        "CoredumpFilter": "0x33",
        "DefaultDependencies": "yes",
        "DefaultMemoryLow": "0",
        "DefaultMemoryMin": "0",
        "Delegate": "no",
        "Description": "started.service",
        "DevicePolicy": "auto",
        "DynamicUser": "no",
        "ExecMainCode": "0",
        "ExecMainExitTimestampMonotonic": "0",
        "ExecMainPID": "0",
        "ExecMainStartTimestampMonotonic": "0",
        "ExecMainStatus": "0",
        "ExitType": "main",
        "FailureAction": "none",
        "FileDescriptorStoreMax": "0",
        "FinalKillSignal": "9",
        "FreezerState": "running",
        "GID": "[not set]",
        "GuessMainPID": "yes",
        "IOAccounting": "no",
        "IOReadBytes": "18446744073709551615",
        "IOReadOperations": "18446744073709551615",
        "IOSchedulingClass": "2",
        "IOSchedulingPriority": "4",
        "IOWeight": "[not set]",
        "IOWriteBytes": "18446744073709551615",
        "IOWriteOperations": "18446744073709551615",
        "IPAccounting": "no",
        "IPEgressBytes": "[no data]",
        "IPEgressPackets": "[no data]",
        "IPIngressBytes": "[no data]",
        "IPIngressPackets": "[no data]",
        "Id": "started.service",
        "IgnoreOnIsolate": "no",
        "IgnoreSIGPIPE": "yes",
        "InactiveEnterTimestampMonotonic": "0",
        "InactiveExitTimestampMonotonic": "0",
        "JobRunningTimeoutUSec": "infinity",
        "JobTimeoutAction": "none",
        "JobTimeoutUSec": "infinity",
        "KeyringMode": "private",
        "KillMode": "control-group",
        "KillSignal": "15",
        "LimitAS": "infinity",
        "LimitASSoft": "infinity",
        "LimitCORE": "infinity",
        "LimitCORESoft": "0",
        "LimitCPU": "infinity",
        "LimitCPUSoft": "infinity",
        "LimitDATA": "infinity",
        "LimitDATASoft": "infinity",
        "LimitFSIZE": "infinity",
        "LimitFSIZESoft": "infinity",
        "LimitLOCKS": "infinity",
        "LimitLOCKSSoft": "infinity",
        "LimitMEMLOCK": "512135168",
        "LimitMEMLOCKSoft": "512135168",
        "LimitMSGQUEUE": "819200",
        "LimitMSGQUEUESoft": "819200",
        "LimitNICE": "0",
        "LimitNICESoft": "0",
        "LimitNOFILE": "1048576",
        "LimitNOFILESoft": "1048576",
        "LimitNPROC": "15336",
        "LimitNPROCSoft": "15336",
        "LimitRSS": "infinity",
        "LimitRSSSoft": "infinity",
        "LimitRTPRIO": "0",
        "LimitRTPRIOSoft": "0",
        "LimitRTTIME": "infinity",
        "LimitRTTIMESoft": "infinity",
        "LimitSIGPENDING": "15336",
        "LimitSIGPENDINGSoft": "15336",
        "LimitSTACK": "infinity",
        "LimitSTACKSoft": "8388608",
        "LoadError": "org.freedesktop.systemd1.NoSuchUnit \"Unit started.service not found.\"",
        "LoadState": "not-found",
        "LockPersonality": "no",
        "LogLevelMax": "-1",
        "LogRateLimitBurst": "0",
        "LogRateLimitIntervalUSec": "0",
        "LogsDirectoryMode": "0755",
        "MainPID": "0",
        "ManagedOOMMemoryPressure": "auto",
        "ManagedOOMMemoryPressureLimit": "0",
        "ManagedOOMPreference": "none",
        "ManagedOOMSwap": "auto",
        "MemoryAccounting": "yes",
        "MemoryAvailable": "infinity",
        "MemoryCurrent": "[not set]",
        "MemoryDenyWriteExecute": "no",
        "MemoryHigh": "infinity",
        "MemoryLimit": "infinity",
        "MemoryLow": "0",
        "MemoryMax": "infinity",
        "MemoryMin": "0",
        "MemorySwapMax": "infinity",
        "MountAPIVFS": "no",
        "NFileDescriptorStore": "0",
        "NRestarts": "0",
        "NUMAPolicy": "n/a",
        "Names": "started.service",
        "NeedDaemonReload": "no",
        "Nice": "0",
        "NoNewPrivileges": "no",
        "NonBlocking": "no",
        "NotifyAccess": "none",
        "OOMScoreAdjust": "0",
        "OnFailureJobMode": "replace",
        "OnSuccessJobMode": "fail",
        "Perpetual": "no",
        "PrivateDevices": "no",
        "PrivateIPC": "no",
        "PrivateMounts": "no",
        "PrivateNetwork": "no",
        "PrivateTmp": "no",
        "PrivateUsers": "no",
        "ProcSubset": "all",
        "ProtectClock": "no",
        "ProtectControlGroups": "no",
        "ProtectHome": "no",
        "ProtectHostname": "no",
        "ProtectKernelLogs": "no",
        "ProtectKernelModules": "no",
        "ProtectKernelTunables": "no",
        "ProtectProc": "default",
        "ProtectSystem": "no",
        "RefuseManualStart": "no",
        "RefuseManualStop": "no",
        "ReloadResult": "success",
        "RemainAfterExit": "no",
        "RemoveIPC": "no",
        "Restart": "no",
        "RestartKillSignal": "15",
        "RestartUSec": "100ms",
        "RestrictNamespaces": "no",
        "RestrictRealtime": "no",
        "RestrictSUIDSGID": "no",
        "Result": "success",
        "RootDirectoryStartOnly": "no",
        "RuntimeDirectoryMode": "0755",
        "RuntimeDirectoryPreserve": "no",
        "RuntimeMaxUSec": "infinity",
        "RuntimeRandomizedExtraUSec": "0",
        "SameProcessGroup": "no",
        "SecureBits": "0",
        "SendSIGHUP": "no",
        "SendSIGKILL": "yes",
        "StandardError": "inherit",
        "StandardInput": "null",
        "StandardOutput": "inherit",
        "StartLimitAction": "none",
        "StartLimitBurst": "5",
        "StartLimitIntervalUSec": "10s",
        "StartupBlockIOWeight": "[not set]",
        "StartupCPUShares": "[not set]",
        "StartupCPUWeight": "[not set]",
        "StartupIOWeight": "[not set]",
        "StateChangeTimestampMonotonic": "0",
        "StateDirectoryMode": "0755",
        "StatusErrno": "0",
        "StopWhenUnneeded": "no",
        "SubState": "dead",
        "SuccessAction": "none",
        "SyslogFacility": "3",
        "SyslogLevel": "6",
        "SyslogLevelPrefix": "yes",
        "SyslogPriority": "30",
        "SystemCallErrorNumber": "2147483646",
        "TTYReset": "no",
        "TTYVHangup": "no",
        "TTYVTDisallocate": "no",
        "TasksAccounting": "yes",
        "TasksCurrent": "[not set]",
        "TasksMax": "4600",
        "TimeoutAbortUSec": "1min 30s",
        "TimeoutCleanUSec": "infinity",
        "TimeoutStartFailureMode": "terminate",
        "TimeoutStartUSec": "1min 30s",
        "TimeoutStopFailureMode": "terminate",
        "TimeoutStopUSec": "1min 30s",
        "TimerSlackNSec": "50000",
        "Transient": "no",
        "UID": "[not set]",
        "UMask": "0022",
        "UtmpMode": "init",
        "WatchdogSignal": "6",
        "WatchdogTimestampMonotonic": "0",
        "WatchdogUSec": "infinity"
    }
}
192.168.122.46 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "name": "started",
    "status": {
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "inactive",
        "AllowIsolate": "no",
        "AssertResult": "no",
        "AssertTimestampMonotonic": "0",
        "BlockIOAccounting": "no",
        "BlockIOWeight": "[not set]",
        "CPUAccounting": "yes",
        "CPUAffinityFromNUMA": "no",
        "CPUQuotaPerSecUSec": "infinity",
        "CPUQuotaPeriodUSec": "infinity",
        "CPUSchedulingPolicy": "0",
        "CPUSchedulingPriority": "0",
        "CPUSchedulingResetOnFork": "no",
        "CPUShares": "[not set]",
        "CPUUsageNSec": "[not set]",
        "CPUWeight": "[not set]",
        "CacheDirectoryMode": "0755",
        "CanFreeze": "yes",
        "CanIsolate": "no",
        "CanReload": "no",
        "CanStart": "no",
        "CanStop": "yes",
        "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon cap_bpf cap_checkpoint_restore",
        "CleanResult": "success",
        "CollectMode": "inactive",
        "ConditionResult": "no",
        "ConditionTimestampMonotonic": "0",
        "ConfigurationDirectoryMode": "0755",
        "ControlGroupId": "0",
        "ControlPID": "0",
        "CoredumpFilter": "0x33",
        "DefaultDependencies": "yes",
        "DefaultMemoryLow": "0",
        "DefaultMemoryMin": "0",
        "Delegate": "no",
        "Description": "started.service",
        "DevicePolicy": "auto",
        "DynamicUser": "no",
        "ExecMainCode": "0",
        "ExecMainExitTimestampMonotonic": "0",
        "ExecMainPID": "0",
        "ExecMainStartTimestampMonotonic": "0",
        "ExecMainStatus": "0",
        "ExitType": "main",
        "FailureAction": "none",
        "FileDescriptorStoreMax": "0",
        "FinalKillSignal": "9",
        "FreezerState": "running",
        "GID": "[not set]",
        "GuessMainPID": "yes",
        "IOAccounting": "no",
        "IOReadBytes": "18446744073709551615",
        "IOReadOperations": "18446744073709551615",
        "IOSchedulingClass": "2",
        "IOSchedulingPriority": "4",
        "IOWeight": "[not set]",
        "IOWriteBytes": "18446744073709551615",
        "IOWriteOperations": "18446744073709551615",
        "IPAccounting": "no",
        "IPEgressBytes": "[no data]",
        "IPEgressPackets": "[no data]",
        "IPIngressBytes": "[no data]",
        "IPIngressPackets": "[no data]",
        "Id": "started.service",
        "IgnoreOnIsolate": "no",
        "IgnoreSIGPIPE": "yes",
        "InactiveEnterTimestampMonotonic": "0",
        "InactiveExitTimestampMonotonic": "0",
        "JobRunningTimeoutUSec": "infinity",
        "JobTimeoutAction": "none",
        "JobTimeoutUSec": "infinity",
        "KeyringMode": "private",
        "KillMode": "control-group",
        "KillSignal": "15",
        "LimitAS": "infinity",
        "LimitASSoft": "infinity",
        "LimitCORE": "infinity",
        "LimitCORESoft": "0",
        "LimitCPU": "infinity",
        "LimitCPUSoft": "infinity",
        "LimitDATA": "infinity",
        "LimitDATASoft": "infinity",
        "LimitFSIZE": "infinity",
        "LimitFSIZESoft": "infinity",
        "LimitLOCKS": "infinity",
        "LimitLOCKSSoft": "infinity",
        "LimitMEMLOCK": "512135168",
        "LimitMEMLOCKSoft": "512135168",
        "LimitMSGQUEUE": "819200",
        "LimitMSGQUEUESoft": "819200",
        "LimitNICE": "0",
        "LimitNICESoft": "0",
        "LimitNOFILE": "1048576",
        "LimitNOFILESoft": "1048576",
        "LimitNPROC": "15336",
        "LimitNPROCSoft": "15336",
        "LimitRSS": "infinity",
        "LimitRSSSoft": "infinity",
        "LimitRTPRIO": "0",
        "LimitRTPRIOSoft": "0",
        "LimitRTTIME": "infinity",
        "LimitRTTIMESoft": "infinity",
        "LimitSIGPENDING": "15336",
        "LimitSIGPENDINGSoft": "15336",
        "LimitSTACK": "infinity",
        "LimitSTACKSoft": "8388608",
        "LoadError": "org.freedesktop.systemd1.NoSuchUnit \"Unit started.service not found.\"",
        "LoadState": "not-found",
        "LockPersonality": "no",
        "LogLevelMax": "-1",
        "LogRateLimitBurst": "0",
        "LogRateLimitIntervalUSec": "0",
        "LogsDirectoryMode": "0755",
        "MainPID": "0",
        "ManagedOOMMemoryPressure": "auto",
        "ManagedOOMMemoryPressureLimit": "0",
        "ManagedOOMPreference": "none",
        "ManagedOOMSwap": "auto",
        "MemoryAccounting": "yes",
        "MemoryAvailable": "infinity",
        "MemoryCurrent": "[not set]",
        "MemoryDenyWriteExecute": "no",
        "MemoryHigh": "infinity",
        "MemoryLimit": "infinity",
        "MemoryLow": "0",
        "MemoryMax": "infinity",
        "MemoryMin": "0",
        "MemorySwapMax": "infinity",
        "MountAPIVFS": "no",
        "NFileDescriptorStore": "0",
        "NRestarts": "0",
        "NUMAPolicy": "n/a",
        "Names": "started.service",
        "NeedDaemonReload": "no",
        "Nice": "0",
        "NoNewPrivileges": "no",
        "NonBlocking": "no",
        "NotifyAccess": "none",
        "OOMScoreAdjust": "0",
        "OnFailureJobMode": "replace",
        "OnSuccessJobMode": "fail",
        "Perpetual": "no",
        "PrivateDevices": "no",
        "PrivateIPC": "no",
        "PrivateMounts": "no",
        "PrivateNetwork": "no",
        "PrivateTmp": "no",
        "PrivateUsers": "no",
        "ProcSubset": "all",
        "ProtectClock": "no",
        "ProtectControlGroups": "no",
        "ProtectHome": "no",
        "ProtectHostname": "no",
        "ProtectKernelLogs": "no",
        "ProtectKernelModules": "no",
        "ProtectKernelTunables": "no",
        "ProtectProc": "default",
        "ProtectSystem": "no",
        "RefuseManualStart": "no",
        "RefuseManualStop": "no",
        "ReloadResult": "success",
        "RemainAfterExit": "no",
        "RemoveIPC": "no",
        "Restart": "no",
        "RestartKillSignal": "15",
        "RestartUSec": "100ms",
        "RestrictNamespaces": "no",
        "RestrictRealtime": "no",
        "RestrictSUIDSGID": "no",
        "Result": "success",
        "RootDirectoryStartOnly": "no",
        "RuntimeDirectoryMode": "0755",
        "RuntimeDirectoryPreserve": "no",
        "RuntimeMaxUSec": "infinity",
        "RuntimeRandomizedExtraUSec": "0",
        "SameProcessGroup": "no",
        "SecureBits": "0",
        "SendSIGHUP": "no",
        "SendSIGKILL": "yes",
        "StandardError": "inherit",
        "StandardInput": "null",
        "StandardOutput": "inherit",
        "StartLimitAction": "none",
        "StartLimitBurst": "5",
        "StartLimitIntervalUSec": "10s",
        "StartupBlockIOWeight": "[not set]",
        "StartupCPUShares": "[not set]",
        "StartupCPUWeight": "[not set]",
        "StartupIOWeight": "[not set]",
        "StateChangeTimestampMonotonic": "0",
        "StateDirectoryMode": "0755",
        "StatusErrno": "0",
        "StopWhenUnneeded": "no",
        "SubState": "dead",
        "SuccessAction": "none",
        "SyslogFacility": "3",
        "SyslogLevel": "6",
        "SyslogLevelPrefix": "yes",
        "SyslogPriority": "30",
        "SystemCallErrorNumber": "2147483646",
        "TTYReset": "no",
        "TTYVHangup": "no",
        "TTYVTDisallocate": "no",
        "TasksAccounting": "yes",
        "TasksCurrent": "[not set]",
        "TasksMax": "4600",
        "TimeoutAbortUSec": "1min 30s",
        "TimeoutCleanUSec": "infinity",
        "TimeoutStartFailureMode": "terminate",
        "TimeoutStartUSec": "1min 30s",
        "TimeoutStopFailureMode": "terminate",
        "TimeoutStopUSec": "1min 30s",
        "TimerSlackNSec": "50000",
        "Transient": "no",
        "UID": "[not set]",
        "UMask": "0022",
        "UtmpMode": "init",
        "WatchdogSignal": "6",
        "WatchdogTimestampMonotonic": "0",
        "WatchdogUSec": "infinity"
    }
}
```

- - Verifying status using `ansible demoByYash -b -m service -a "name=chessx service=status"`
```
[WARNING]: Both option name and its alias service are set.
192.168.122.128 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "name": "status",
    "status": {
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "inactive",
        "AllowIsolate": "no",
        "AssertResult": "no",
        "AssertTimestampMonotonic": "0",
        "BlockIOAccounting": "no",
        "BlockIOWeight": "[not set]",
        "CPUAccounting": "yes",
        "CPUAffinityFromNUMA": "no",
        "CPUQuotaPerSecUSec": "infinity",
        "CPUQuotaPeriodUSec": "infinity",
        "CPUSchedulingPolicy": "0",
        "CPUSchedulingPriority": "0",
        "CPUSchedulingResetOnFork": "no",
        "CPUShares": "[not set]",
        "CPUUsageNSec": "[not set]",
        "CPUWeight": "[not set]",
        "CacheDirectoryMode": "0755",
        "CanFreeze": "yes",
        "CanIsolate": "no",
        "CanReload": "no",
        "CanStart": "no",
        "CanStop": "yes",
        "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon cap_bpf cap_checkpoint_restore",
        "CleanResult": "success",
        "CollectMode": "inactive",
        "ConditionResult": "no",
        "ConditionTimestampMonotonic": "0",
        "ConfigurationDirectoryMode": "0755",
        "ControlGroupId": "0",
        "ControlPID": "0",
        "CoredumpFilter": "0x33",
        "DefaultDependencies": "yes",
        "DefaultMemoryLow": "0",
        "DefaultMemoryMin": "0",
        "Delegate": "no",
        "Description": "status.service",
        "DevicePolicy": "auto",
        "DynamicUser": "no",
        "ExecMainCode": "0",
        "ExecMainExitTimestampMonotonic": "0",
        "ExecMainPID": "0",
        "ExecMainStartTimestampMonotonic": "0",
        "ExecMainStatus": "0",
        "ExitType": "main",
        "FailureAction": "none",
        "FileDescriptorStoreMax": "0",
        "FinalKillSignal": "9",
        "FreezerState": "running",
        "GID": "[not set]",
        "GuessMainPID": "yes",
        "IOAccounting": "no",
        "IOReadBytes": "18446744073709551615",
        "IOReadOperations": "18446744073709551615",
        "IOSchedulingClass": "2",
        "IOSchedulingPriority": "4",
        "IOWeight": "[not set]",
        "IOWriteBytes": "18446744073709551615",
        "IOWriteOperations": "18446744073709551615",
        "IPAccounting": "no",
        "IPEgressBytes": "[no data]",
        "IPEgressPackets": "[no data]",
        "IPIngressBytes": "[no data]",
        "IPIngressPackets": "[no data]",
        "Id": "status.service",
        "IgnoreOnIsolate": "no",
        "IgnoreSIGPIPE": "yes",
        "InactiveEnterTimestampMonotonic": "0",
        "InactiveExitTimestampMonotonic": "0",
        "JobRunningTimeoutUSec": "infinity",
        "JobTimeoutAction": "none",
        "JobTimeoutUSec": "infinity",
        "KeyringMode": "private",
        "KillMode": "control-group",
        "KillSignal": "15",
        "LimitAS": "infinity",
        "LimitASSoft": "infinity",
        "LimitCORE": "infinity",
        "LimitCORESoft": "0",
        "LimitCPU": "infinity",
        "LimitCPUSoft": "infinity",
        "LimitDATA": "infinity",
        "LimitDATASoft": "infinity",
        "LimitFSIZE": "infinity",
        "LimitFSIZESoft": "infinity",
        "LimitLOCKS": "infinity",
        "LimitLOCKSSoft": "infinity",
        "LimitMEMLOCK": "512135168",
        "LimitMEMLOCKSoft": "512135168",
        "LimitMSGQUEUE": "819200",
        "LimitMSGQUEUESoft": "819200",
        "LimitNICE": "0",
        "LimitNICESoft": "0",
        "LimitNOFILE": "1048576",
        "LimitNOFILESoft": "1048576",
        "LimitNPROC": "15336",
        "LimitNPROCSoft": "15336",
        "LimitRSS": "infinity",
        "LimitRSSSoft": "infinity",
        "LimitRTPRIO": "0",
        "LimitRTPRIOSoft": "0",
        "LimitRTTIME": "infinity",
        "LimitRTTIMESoft": "infinity",
        "LimitSIGPENDING": "15336",
        "LimitSIGPENDINGSoft": "15336",
        "LimitSTACK": "infinity",
        "LimitSTACKSoft": "8388608",
        "LoadError": "org.freedesktop.systemd1.NoSuchUnit \"Unit status.service not found.\"",
        "LoadState": "not-found",
        "LockPersonality": "no",
        "LogLevelMax": "-1",
        "LogRateLimitBurst": "0",
        "LogRateLimitIntervalUSec": "0",
        "LogsDirectoryMode": "0755",
        "MainPID": "0",
        "ManagedOOMMemoryPressure": "auto",
        "ManagedOOMMemoryPressureLimit": "0",
        "ManagedOOMPreference": "none",
        "ManagedOOMSwap": "auto",
        "MemoryAccounting": "yes",
        "MemoryAvailable": "infinity",
        "MemoryCurrent": "[not set]",
        "MemoryDenyWriteExecute": "no",
        "MemoryHigh": "infinity",
        "MemoryLimit": "infinity",
        "MemoryLow": "0",
        "MemoryMax": "infinity",
        "MemoryMin": "0",
        "MemorySwapMax": "infinity",
        "MountAPIVFS": "no",
        "NFileDescriptorStore": "0",
        "NRestarts": "0",
        "NUMAPolicy": "n/a",
        "Names": "status.service",
        "NeedDaemonReload": "no",
        "Nice": "0",
        "NoNewPrivileges": "no",
        "NonBlocking": "no",
        "NotifyAccess": "none",
        "OOMScoreAdjust": "0",
        "OnFailureJobMode": "replace",
        "OnSuccessJobMode": "fail",
        "Perpetual": "no",
        "PrivateDevices": "no",
        "PrivateIPC": "no",
        "PrivateMounts": "no",
        "PrivateNetwork": "no",
        "PrivateTmp": "no",
        "PrivateUsers": "no",
        "ProcSubset": "all",
        "ProtectClock": "no",
        "ProtectControlGroups": "no",
        "ProtectHome": "no",
        "ProtectHostname": "no",
        "ProtectKernelLogs": "no",
        "ProtectKernelModules": "no",
        "ProtectKernelTunables": "no",
        "ProtectProc": "default",
        "ProtectSystem": "no",
        "RefuseManualStart": "no",
        "RefuseManualStop": "no",
        "ReloadResult": "success",
        "RemainAfterExit": "no",
        "RemoveIPC": "no",
        "Restart": "no",
        "RestartKillSignal": "15",
        "RestartUSec": "100ms",
        "RestrictNamespaces": "no",
        "RestrictRealtime": "no",
        "RestrictSUIDSGID": "no",
        "Result": "success",
        "RootDirectoryStartOnly": "no",
        "RuntimeDirectoryMode": "0755",
        "RuntimeDirectoryPreserve": "no",
        "RuntimeMaxUSec": "infinity",
        "RuntimeRandomizedExtraUSec": "0",
        "SameProcessGroup": "no",
        "SecureBits": "0",
        "SendSIGHUP": "no",
        "SendSIGKILL": "yes",
        "StandardError": "inherit",
        "StandardInput": "null",
        "StandardOutput": "inherit",
        "StartLimitAction": "none",
        "StartLimitBurst": "5",
        "StartLimitIntervalUSec": "10s",
        "StartupBlockIOWeight": "[not set]",
        "StartupCPUShares": "[not set]",
        "StartupCPUWeight": "[not set]",
        "StartupIOWeight": "[not set]",
        "StateChangeTimestampMonotonic": "0",
        "StateDirectoryMode": "0755",
        "StatusErrno": "0",
        "StopWhenUnneeded": "no",
        "SubState": "dead",
        "SuccessAction": "none",
        "SyslogFacility": "3",
        "SyslogLevel": "6",
        "SyslogLevelPrefix": "yes",
        "SyslogPriority": "30",
        "SystemCallErrorNumber": "2147483646",
        "TTYReset": "no",
        "TTYVHangup": "no",
        "TTYVTDisallocate": "no",
        "TasksAccounting": "yes",
        "TasksCurrent": "[not set]",
        "TasksMax": "4600",
        "TimeoutAbortUSec": "1min 30s",
        "TimeoutCleanUSec": "infinity",
        "TimeoutStartFailureMode": "terminate",
        "TimeoutStartUSec": "1min 30s",
        "TimeoutStopFailureMode": "terminate",
        "TimeoutStopUSec": "1min 30s",
        "TimerSlackNSec": "50000",
        "Transient": "no",
        "UID": "[not set]",
        "UMask": "0022",
        "UtmpMode": "init",
        "WatchdogSignal": "6",
        "WatchdogTimestampMonotonic": "0",
        "WatchdogUSec": "infinity"
    }
}
192.168.122.46 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "name": "status",
    "status": {
        "ActiveEnterTimestampMonotonic": "0",
        "ActiveExitTimestampMonotonic": "0",
        "ActiveState": "inactive",
        "AllowIsolate": "no",
        "AssertResult": "no",
        "AssertTimestampMonotonic": "0",
        "BlockIOAccounting": "no",
        "BlockIOWeight": "[not set]",
        "CPUAccounting": "yes",
        "CPUAffinityFromNUMA": "no",
        "CPUQuotaPerSecUSec": "infinity",
        "CPUQuotaPeriodUSec": "infinity",
        "CPUSchedulingPolicy": "0",
        "CPUSchedulingPriority": "0",
        "CPUSchedulingResetOnFork": "no",
        "CPUShares": "[not set]",
        "CPUUsageNSec": "[not set]",
        "CPUWeight": "[not set]",
        "CacheDirectoryMode": "0755",
        "CanFreeze": "yes",
        "CanIsolate": "no",
        "CanReload": "no",
        "CanStart": "no",
        "CanStop": "yes",
        "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon cap_bpf cap_checkpoint_restore",
        "CleanResult": "success",
        "CollectMode": "inactive",
        "ConditionResult": "no",
        "ConditionTimestampMonotonic": "0",
        "ConfigurationDirectoryMode": "0755",
        "ControlGroupId": "0",
        "ControlPID": "0",
        "CoredumpFilter": "0x33",
        "DefaultDependencies": "yes",
        "DefaultMemoryLow": "0",
        "DefaultMemoryMin": "0",
        "Delegate": "no",
        "Description": "status.service",
        "DevicePolicy": "auto",
        "DynamicUser": "no",
        "ExecMainCode": "0",
        "ExecMainExitTimestampMonotonic": "0",
        "ExecMainPID": "0",
        "ExecMainStartTimestampMonotonic": "0",
        "ExecMainStatus": "0",
        "ExitType": "main",
        "FailureAction": "none",
        "FileDescriptorStoreMax": "0",
        "FinalKillSignal": "9",
        "FreezerState": "running",
        "GID": "[not set]",
        "GuessMainPID": "yes",
        "IOAccounting": "no",
        "IOReadBytes": "18446744073709551615",
        "IOReadOperations": "18446744073709551615",
        "IOSchedulingClass": "2",
        "IOSchedulingPriority": "4",
        "IOWeight": "[not set]",
        "IOWriteBytes": "18446744073709551615",
        "IOWriteOperations": "18446744073709551615",
        "IPAccounting": "no",
        "IPEgressBytes": "[no data]",
        "IPEgressPackets": "[no data]",
        "IPIngressBytes": "[no data]",
        "IPIngressPackets": "[no data]",
        "Id": "status.service",
        "IgnoreOnIsolate": "no",
        "IgnoreSIGPIPE": "yes",
        "InactiveEnterTimestampMonotonic": "0",
        "InactiveExitTimestampMonotonic": "0",
        "JobRunningTimeoutUSec": "infinity",
        "JobTimeoutAction": "none",
        "JobTimeoutUSec": "infinity",
        "KeyringMode": "private",
        "KillMode": "control-group",
        "KillSignal": "15",
        "LimitAS": "infinity",
        "LimitASSoft": "infinity",
        "LimitCORE": "infinity",
        "LimitCORESoft": "0",
        "LimitCPU": "infinity",
        "LimitCPUSoft": "infinity",
        "LimitDATA": "infinity",
        "LimitDATASoft": "infinity",
        "LimitFSIZE": "infinity",
        "LimitFSIZESoft": "infinity",
        "LimitLOCKS": "infinity",
        "LimitLOCKSSoft": "infinity",
        "LimitMEMLOCK": "512135168",
        "LimitMEMLOCKSoft": "512135168",
        "LimitMSGQUEUE": "819200",
        "LimitMSGQUEUESoft": "819200",
        "LimitNICE": "0",
        "LimitNICESoft": "0",
        "LimitNOFILE": "1048576",
        "LimitNOFILESoft": "1048576",
        "LimitNPROC": "15336",
        "LimitNPROCSoft": "15336",
        "LimitRSS": "infinity",
        "LimitRSSSoft": "infinity",
        "LimitRTPRIO": "0",
        "LimitRTPRIOSoft": "0",
        "LimitRTTIME": "infinity",
        "LimitRTTIMESoft": "infinity",
        "LimitSIGPENDING": "15336",
        "LimitSIGPENDINGSoft": "15336",
        "LimitSTACK": "infinity",
        "LimitSTACKSoft": "8388608",
        "LoadError": "org.freedesktop.systemd1.NoSuchUnit \"Unit status.service not found.\"",
        "LoadState": "not-found",
        "LockPersonality": "no",
        "LogLevelMax": "-1",
        "LogRateLimitBurst": "0",
        "LogRateLimitIntervalUSec": "0",
        "LogsDirectoryMode": "0755",
        "MainPID": "0",
        "ManagedOOMMemoryPressure": "auto",
        "ManagedOOMMemoryPressureLimit": "0",
        "ManagedOOMPreference": "none",
        "ManagedOOMSwap": "auto",
        "MemoryAccounting": "yes",
        "MemoryAvailable": "infinity",
        "MemoryCurrent": "[not set]",
        "MemoryDenyWriteExecute": "no",
        "MemoryHigh": "infinity",
        "MemoryLimit": "infinity",
        "MemoryLow": "0",
        "MemoryMax": "infinity",
        "MemoryMin": "0",
        "MemorySwapMax": "infinity",
        "MountAPIVFS": "no",
        "NFileDescriptorStore": "0",
        "NRestarts": "0",
        "NUMAPolicy": "n/a",
        "Names": "status.service",
        "NeedDaemonReload": "no",
        "Nice": "0",
        "NoNewPrivileges": "no",
        "NonBlocking": "no",
        "NotifyAccess": "none",
        "OOMScoreAdjust": "0",
        "OnFailureJobMode": "replace",
        "OnSuccessJobMode": "fail",
        "Perpetual": "no",
        "PrivateDevices": "no",
        "PrivateIPC": "no",
        "PrivateMounts": "no",
        "PrivateNetwork": "no",
        "PrivateTmp": "no",
        "PrivateUsers": "no",
        "ProcSubset": "all",
        "ProtectClock": "no",
        "ProtectControlGroups": "no",
        "ProtectHome": "no",
        "ProtectHostname": "no",
        "ProtectKernelLogs": "no",
        "ProtectKernelModules": "no",
        "ProtectKernelTunables": "no",
        "ProtectProc": "default",
        "ProtectSystem": "no",
        "RefuseManualStart": "no",
        "RefuseManualStop": "no",
        "ReloadResult": "success",
        "RemainAfterExit": "no",
        "RemoveIPC": "no",
        "Restart": "no",
        "RestartKillSignal": "15",
        "RestartUSec": "100ms",
        "RestrictNamespaces": "no",
        "RestrictRealtime": "no",
        "RestrictSUIDSGID": "no",
        "Result": "success",
        "RootDirectoryStartOnly": "no",
        "RuntimeDirectoryMode": "0755",
        "RuntimeDirectoryPreserve": "no",
        "RuntimeMaxUSec": "infinity",
        "RuntimeRandomizedExtraUSec": "0",
        "SameProcessGroup": "no",
        "SecureBits": "0",
        "SendSIGHUP": "no",
        "SendSIGKILL": "yes",
        "StandardError": "inherit",
        "StandardInput": "null",
        "StandardOutput": "inherit",
        "StartLimitAction": "none",
        "StartLimitBurst": "5",
        "StartLimitIntervalUSec": "10s",
        "StartupBlockIOWeight": "[not set]",
        "StartupCPUShares": "[not set]",
        "StartupCPUWeight": "[not set]",
        "StartupIOWeight": "[not set]",
        "StateChangeTimestampMonotonic": "0",
        "StateDirectoryMode": "0755",
        "StatusErrno": "0",
        "StopWhenUnneeded": "no",
        "SubState": "dead",
        "SuccessAction": "none",
        "SyslogFacility": "3",
        "SyslogLevel": "6",
        "SyslogLevelPrefix": "yes",
        "SyslogPriority": "30",
        "SystemCallErrorNumber": "2147483646",
        "TTYReset": "no",
        "TTYVHangup": "no",
        "TTYVTDisallocate": "no",
        "TasksAccounting": "yes",
        "TasksCurrent": "[not set]",
        "TasksMax": "4600",
        "TimeoutAbortUSec": "1min 30s",
        "TimeoutCleanUSec": "infinity",
        "TimeoutStartFailureMode": "terminate",
        "TimeoutStartUSec": "1min 30s",
        "TimeoutStopFailureMode": "terminate",
        "TimeoutStopUSec": "1min 30s",
        "TimerSlackNSec": "50000",
        "Transient": "no",
        "UID": "[not set]",
        "UMask": "0022",
        "UtmpMode": "init",
        "WatchdogSignal": "6",
        "WatchdogTimestampMonotonic": "0",
        "WatchdogUSec": "infinity"
    }
}
```

- Uninstalling using apt module: 
a. ansible demoByYash -b -m apt -a "name=chessx state=absent"
```
192.168.122.128 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "stderr": "",
    "stderr_lines": [],
    "stdout": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nThe following packages were automatically installed and are no longer required:\n  libdouble-conversion3 libmd4c0 libpcre2-16-0 libqt5core5a libqt5dbus5\n  libqt5gui5 libqt5multimedia5 libqt5network5 libqt5printsupport5 libqt5qml5\n  libqt5qmlmodels5 libqt5quick5 libqt5svg5 libqt5waylandclient5\n  libqt5waylandcompositor5 libqt5widgets5 libqt5xml5 libxcb-xinerama0\n  libxcb-xinput0 qt5-gtk-platformtheme qttranslations5-l10n qtwayland5\n  stockfish\nUse 'sudo apt autoremove' to remove them.\nThe following packages will be REMOVED:\n  chessx\n0 upgraded, 0 newly installed, 1 to remove and 63 not upgraded.\nAfter this operation, 6885 kB disk space will be freed.\n(Reading database ... \r(Reading database ... 5%\r(Reading database ... 10%\r(Reading database ... 15%\r(Reading database ... 20%\r(Reading database ... 25%\r(Reading database ... 30%\r(Reading database ... 35%\r(Reading database ... 40%\r(Reading database ... 45%\r(Reading database ... 50%\r(Reading database ... 55%\r(Reading database ... 60%\r(Reading database ... 65%\r(Reading database ... 70%\r(Reading database ... 75%\r(Reading database ... 80%\r(Reading database ... 85%\r(Reading database ... 90%\r(Reading database ... 95%\r(Reading database ... 100%\r(Reading database ... 327132 files and directories currently installed.)\r\nRemoving chessx (1.4.6-2build1) ...\r\nProcessing triggers for gnome-menus (3.36.0-1.1ubuntu1) ...\r\nProcessing triggers for man-db (2.11.2-1) ...\r\nProcessing triggers for mailcap (3.70+nmu1ubuntu1) ...\r\nProcessing triggers for desktop-file-utils (0.26-1ubuntu5) ...\r\n",
    "stdout_lines": [
        "Reading package lists...",
        "Building dependency tree...",
        "Reading state information...",
        "The following packages were automatically installed and are no longer required:",
        "  libdouble-conversion3 libmd4c0 libpcre2-16-0 libqt5core5a libqt5dbus5",
        "  libqt5gui5 libqt5multimedia5 libqt5network5 libqt5printsupport5 libqt5qml5",
        "  libqt5qmlmodels5 libqt5quick5 libqt5svg5 libqt5waylandclient5",
        "  libqt5waylandcompositor5 libqt5widgets5 libqt5xml5 libxcb-xinerama0",
        "  libxcb-xinput0 qt5-gtk-platformtheme qttranslations5-l10n qtwayland5",
        "  stockfish",
        "Use 'sudo apt autoremove' to remove them.",
        "The following packages will be REMOVED:",
        "  chessx",
        "0 upgraded, 0 newly installed, 1 to remove and 63 not upgraded.",
        "After this operation, 6885 kB disk space will be freed.",
        "(Reading database ... ",
        "(Reading database ... 5%",
        "(Reading database ... 10%",
        "(Reading database ... 15%",
        "(Reading database ... 20%",
        "(Reading database ... 25%",
        "(Reading database ... 30%",
        "(Reading database ... 35%",
        "(Reading database ... 40%",
        "(Reading database ... 45%",
        "(Reading database ... 50%",
        "(Reading database ... 55%",
        "(Reading database ... 60%",
        "(Reading database ... 65%",
        "(Reading database ... 70%",
        "(Reading database ... 75%",
        "(Reading database ... 80%",
        "(Reading database ... 85%",
        "(Reading database ... 90%",
        "(Reading database ... 95%",
        "(Reading database ... 100%",
        "(Reading database ... 327132 files and directories currently installed.)",
        "Removing chessx (1.4.6-2build1) ...",
        "Processing triggers for gnome-menus (3.36.0-1.1ubuntu1) ...",
        "Processing triggers for man-db (2.11.2-1) ...",
        "Processing triggers for mailcap (3.70+nmu1ubuntu1) ...",
        "Processing triggers for desktop-file-utils (0.26-1ubuntu5) ..."
    ]
}
192.168.122.46 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "stderr": "",
    "stderr_lines": [],
    "stdout": "Reading package lists...\nBuilding dependency tree...\nReading state information...\nThe following packages were automatically installed and are no longer required:\n  libdouble-conversion3 libmd4c0 libpcre2-16-0 libqt5core5a libqt5dbus5\n  libqt5gui5 libqt5multimedia5 libqt5network5 libqt5printsupport5 libqt5qml5\n  libqt5qmlmodels5 libqt5quick5 libqt5svg5 libqt5waylandclient5\n  libqt5waylandcompositor5 libqt5widgets5 libqt5xml5 libxcb-xinerama0\n  libxcb-xinput0 qt5-gtk-platformtheme qttranslations5-l10n qtwayland5\n  stockfish\nUse 'sudo apt autoremove' to remove them.\nThe following packages will be REMOVED:\n  chessx\n0 upgraded, 0 newly installed, 1 to remove and 68 not upgraded.\nAfter this operation, 6885 kB disk space will be freed.\n(Reading database ... \r(Reading database ... 5%\r(Reading database ... 10%\r(Reading database ... 15%\r(Reading database ... 20%\r(Reading database ... 25%\r(Reading database ... 30%\r(Reading database ... 35%\r(Reading database ... 40%\r(Reading database ... 45%\r(Reading database ... 50%\r(Reading database ... 55%\r(Reading database ... 60%\r(Reading database ... 65%\r(Reading database ... 70%\r(Reading database ... 75%\r(Reading database ... 80%\r(Reading database ... 85%\r(Reading database ... 90%\r(Reading database ... 95%\r(Reading database ... 100%\r(Reading database ... 327132 files and directories currently installed.)\r\nRemoving chessx (1.4.6-2build1) ...\r\nProcessing triggers for gnome-menus (3.36.0-1.1ubuntu1) ...\r\nProcessing triggers for man-db (2.11.2-1) ...\r\nProcessing triggers for mailcap (3.70+nmu1ubuntu1) ...\r\nProcessing triggers for desktop-file-utils (0.26-1ubuntu5) ...\r\n",
    "stdout_lines": [
        "Reading package lists...",
        "Building dependency tree...",
        "Reading state information...",
        "The following packages were automatically installed and are no longer required:",
        "  libdouble-conversion3 libmd4c0 libpcre2-16-0 libqt5core5a libqt5dbus5",
        "  libqt5gui5 libqt5multimedia5 libqt5network5 libqt5printsupport5 libqt5qml5",
        "  libqt5qmlmodels5 libqt5quick5 libqt5svg5 libqt5waylandclient5",
        "  libqt5waylandcompositor5 libqt5widgets5 libqt5xml5 libxcb-xinerama0",
        "  libxcb-xinput0 qt5-gtk-platformtheme qttranslations5-l10n qtwayland5",
        "  stockfish",
        "Use 'sudo apt autoremove' to remove them.",
        "The following packages will be REMOVED:",
        "  chessx",
        "0 upgraded, 0 newly installed, 1 to remove and 68 not upgraded.",
        "After this operation, 6885 kB disk space will be freed.",
        "(Reading database ... ",
        "(Reading database ... 5%",
        "(Reading database ... 10%",
        "(Reading database ... 15%",
        "(Reading database ... 20%",
        "(Reading database ... 25%",
        "(Reading database ... 30%",
        "(Reading database ... 35%",
        "(Reading database ... 40%",
        "(Reading database ... 45%",
        "(Reading database ... 50%",
        "(Reading database ... 55%",
        "(Reading database ... 60%",
        "(Reading database ... 65%",
        "(Reading database ... 70%",
        "(Reading database ... 75%",
        "(Reading database ... 80%",
        "(Reading database ... 85%",
        "(Reading database ... 90%",
        "(Reading database ... 95%",
        "(Reading database ... 100%",
        "(Reading database ... 327132 files and directories currently installed.)",
        "Removing chessx (1.4.6-2build1) ...",
        "Processing triggers for gnome-menus (3.36.0-1.1ubuntu1) ...",
        "Processing triggers for man-db (2.11.2-1) ...",
        "Processing triggers for mailcap (3.70+nmu1ubuntu1) ...",
        "Processing triggers for desktop-file-utils (0.26-1ubuntu5) ..."
    ]
}
```
b. ansible demoByYash -a "which chessx" 
```
192.168.122.46 | FAILED | rc=1 >>
non-zero return code
192.168.122.128 | FAILED | rc=1 >>
non-zero return code
```

- Creating using user module: 
a. ansible demoByYash -m user -b -a "name=YASH"
```
192.168.122.128 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1002,
    "home": "/home/YASH",
    "name": "YASH",
    "shell": "/bin/sh",
    "state": "present",
    "system": false,
    "uid": 1002
}
192.168.122.46 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1002,
    "home": "/home/YASH",
    "name": "YASH",
    "shell": "/bin/sh",
    "state": "present",
    "system": false,
    "uid": 1002
}
```

b. ansible demoByYash -m command -a "cat /etc/passwd" //verifying user creation

```
YASH:x:1002:1002::/home/YASH:/bin/sh
YASH:x:1002:1002::/home/YASH:/bin/sh
```

- Using copy module for copying to server
I first ran `touch fromAnsibleServer` and then
`ansible demoByYash -b -m copy -a "src fromAnsibleServer dest=/tmp"` and got this output:
```
192.168.122.128 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "checksum": "da39a3ee5e6b4b0d3255bfef95601890afd80709",
    "dest": "/tmp/fromAnsibleServer",
    "gid": 0,
    "group": "root",
    "md5sum": "d41d8cd98f00b204e9800998ecf8427e",
    "mode": "0644",
    "owner": "root",
    "size": 0,
    "src": "/home/ansible/.ansible/tmp/ansible-tmp-1701337102.1384983-350231-280001644354507/source",
    "state": "file",
    "uid": 0
}
192.168.122.46 | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "checksum": "da39a3ee5e6b4b0d3255bfef95601890afd80709",
    "dest": "/tmp/fromAnsibleServer",
    "gid": 0,
    "group": "root",
    "md5sum": "d41d8cd98f00b204e9800998ecf8427e",
    "mode": "0644",
    "owner": "root",
    "size": 0,
    "src": "/home/ansible/.ansible/tmp/ansible-tmp-1701337102.0673523-350232-34041638215662/source",
    "state": "file",
    "uid": 0
}
```
b. Verification:
```
ansible demoByYash -b -m shell -a "cd /tmp | ls"
192.168.122.46 | CHANGED | rc=0 >>
created at 5:37
createdFromDell-Latitude
file1
madeFromDELL-LATITUDE-E5470
snap
192.168.122.128 | CHANGED | rc=0 >>
created at 5:37
createdFromDell-Latitude
file1
madeFromDELL-LATITUDE-E5470
snap
```

# Extras 
- Idenpotency present in Playbook & Modules
- HOW DOES IT KNOW things have already been installed WHEN WE TRY TO INSTALL AGAIN?
- We have setup module, which goes to the nodes and find if things already exist - this command runs auto and brings back info of if package exists or not.
- V Imp: `ansible demoByYash -m setup` to be run to find all of the configuration details first
- If filter to be added, `ansible demoByYash -m setup -a "filter=<yourfilter>"` or `ansible demo -m setup -a "filter=RAM"`:
```
192.168.122.46 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false
}
192.168.122.128 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false
}
```

## Playing-Around
- What happens if I add existing nodes to another group? Already know but haven't tried
```
No errors, they get added easily. I added 'test' as a group with exact 2 nodes and it worked:
ansible test --list-hosts
  hosts (2):
    192.168.122.46
    192.168.122.128
```
- Can I add groups with spaces in between? likely not?
```
Ans: I could not:

ansible 'Republic Of India' --list-hosts
[WARNING]:  * Failed to parse /etc/ansible/hosts with yaml plugin: We were
unable to read either as JSON nor YAML, these are the errors we got from each:
JSON: Expecting value: line 1 column 1 (char 0)  Syntax Error while loading
YAML.   did not find expected <document start>  The error appears to be in
'/etc/ansible/hosts': line 13, column 1, but may be elsewhere in the file
depending on the exact syntax problem.  The offending line appears to be:
[REPUBLIC OF INDIA] 192.168.122.46 ^ here
[WARNING]:  * Failed to parse /etc/ansible/hosts with ini plugin:
/etc/ansible/hosts:12: Invalid section entry: '[REPUBLIC OF INDIA]'. Please
make sure that there are no spaces in the section entry, and that there are no
other invalid characters
[WARNING]: Unable to parse /etc/ansible/hosts as an inventory source
[WARNING]: No inventory was parsed, only implicit localhost is available
[WARNING]: provided hosts list is empty, only localhost is available. Note that
the implicit localhost does not match 'all'
[WARNING]: Could not match supplied host pattern, ignoring: Republic
[WARNING]: Could not match supplied host pattern, ignoring: Of
[WARNING]: Could not match supplied host pattern, ignoring: India
```

- What happens if I change the name of group after it has been created in /etc/ansible/hosts file?
```
Not an issue, grouped again easily under the new name.
```
_____________________________________

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
___________________________
<div align = "center">

30 NOV

</div>


https://www.google.com/search?q=Ansible+part+site%3Awww.openvirtualization.pro%2F&sca_esv=586584704&ei=t2FoZejHIIqo2roPgtuguAo&ved=0ahUKEwio_6rov-uCAxUKlFYBHYItCKcQ4dUDCBA&uact=5&oq=Ansible+part+site%3Awww.openvirtualization.pro%2F&gs_lp=Egxnd3Mtd2l6LXNlcnAiLUFuc2libGUgcGFydCBzaXRlOnd3dy5vcGVudmlydHVhbGl6YXRpb24ucHJvL0i5GlCPBljAGHABeACQAQCYAbYCoAG2AqoBAzMtMbgBA8gBAPgBAeIDBBgBIEGIBgE&sclient=gws-wiz-serp

- [Ansible, part I – basics and inventory](https://www.openvirtualization.pro/ansible-part-i-basics-and-inventory/)
- [Ansible, part II – modules and ad-hoc commands](https://www.openvirtualization.pro/ansible-part-ii-modules-and-ad-hoc-commands/)
- [Ansible, part III – YAML and Playbooks](https://www.openvirtualization.pro/ansible-part-iii-yaml-and-playbooks/)

## References
- [Ansible, part III – YAML and Playbooks](https://www.openvirtualization.pro/ansible-part-iii-yaml-and-playbooks/)
- [YouTube Tutorial](https://www.youtube.com/watch?v=uyFrrKju4Es&list=PLBGx66SQNZ8aPsFDwb79JrS2KQBTIZo10&index=34)

## Study Plan
- Playbooks
- Dry Run
- Loops

## Recap
- Ad Hocs don't have idempotency - modules do - no repeatition 
- Ansible knows work has been done due to 'setup' module which is run first auto when a module is run - You won't know it was run!
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
- Run ansible-playbook <playbook>.yaml or for dry run  ansible-playbook <playbook>.yaml --check

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
## Playbooks: Understanding Targets
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
```
Output:
PLAY [demoByYash] ******************************************************************************

TASK [Gathering Facts] *************************************************************************
ok: [192.168.122.46]
ok: [192.168.122.128]

PLAY RECAP *************************************************************************************
192.168.122.128            : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
192.168.122.46             : ok=1    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

## Playbooks: Understanding Tasks
### Playbook 1
- Be wary of indentations, keep task and target on same level
- In vi, the cursor happens on its own
- Planning:
```
---
- hosts: demoByYash
  user: ansible
  become: yes
  connection: ssh
  tasks:
    - name: My first installation using Playbooks
      action: apt name=chessx state=absent
# same as 'ansible demoByYash -b -m apt -a "name=chessx state=present'
...
```
- Run `ansible-playbook <target>.yaml`
- When the above playbook is run again then it won't install the app again due to idempotency
- Be wary of case sensitivity!
- I used ad hoc to verify the installation:
```
ansible demoByYash -m command -a "which chessx"
```

### Playbook 2
Creating playbook that retrieves the IP Address of the servers
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

### Playbook 3
```
Creating playbook that retrieves storage information
---
- hosts: demoByYash
  user: ansible
  tasks:
    - name: getting storage info using df command
      action: command df
      register: myOutput
    - debug: var=myOutput.stdout_lines
...
```

### Playbook 4
Creating a playbook that downloads etcd from GitHub
```
---
- hosts: demoByYash
  user: ansible
  become: yes
  connection: ssh
  gather_facts: yes
  tasks: 
    - name: downloading etcd release
      action: command wget https://github.com/etcd-io/etcd/releases/download/v3.5.10/etcd-v3.5.10-linux-arm64.tar.gz
...
```

## Playbooks: Understanding Variables

- Variables are defined previously to enable flexibility - make changes directly to the vars for later usage
- Define variables before task to loop through set of values, access information like hostname, replace certain strings in templates with values
- Define variable and call it using '{{<variable>}}' in the tasks section
- Example: Using vars can help create templates where user would only have to change the variable value for a playbook for installing anything
```
---
- hosts: demoByYash
  user: ansible #TargetSection till here
  vars:
    - pkg_name: chessx
    - state_name: absent #VariableSection till here
  tasks:
    - name: installing template
      action: apt name='{{pkg_name}}' state='{{state_name}}' #TasksSection till here
...
```
- Emphasis: I did not have to define 'connection' and 'become' in the target section.

## Playbooks: Understanding Handlers
- Handler same as tasks but it has dependencies and only runs when called by first task
- Handlers only work when tasks contain a notify directive and also indicates that it changed something
Lets I want to install an app and then start its service. These are 2 tasks & service start is dependent on installation of file
- notify helps call the handler from the task, like "if conditions met, call the handler"
- Starting service for it does not make sense unless app is installed - This is where handlers come in as they help handle such if-else kind of tasks
```
---
- hosts: demoByYash
  user: ansible
  tasks:
    - name: downloading etcd
      action: command wget https://github.com/etcd-io/etcd/releases/download/v3.5.10/etcd-v3.5.10-linux-amd64.tar.gz
      notify: untar
  handlers:
    - name: untar
      action: command tar -xzvf etcd-v3.5.10-linux-amd64.tar.gz
...
```
- In the above playbook, I download etcd and untar it in the server ONLY IF etcd is downloaded: Power of handelers!

## Playbooks: Understanding Loops
- Doing same steps repeatedly - until same work is done on all servers, keep doing work 
- common ansible loops include changing ownership on several files/directories, creating mulitple files/users, etc.
- But is it correct to call them loops??????? I dont think so since the loop does come to an end at some point

```
---
- hosts: demoByYash
  user: ansible
  become: yes
  connection: ssh
  gather_facts: yes
  tasks:
    - name: adding various users using loops
      command: mkdir '{{item}}' #name='{{item}}' state=present, we couldve done action: user name='{{item}}' state=present as well
      with_items:
        - sonuji
        - rahulji
        - amitji
        - samarthji
...
```
------------------------------------------------
<div align = "center">

# 04 December

</div>

## Topics To Be Covered:
 - Conditions
 - Roles
 - Ansible Vault

## Recap
 - In YAML we have target, task and variable sections, handlers, loops, dry run
 
## Conditions 
 - In prog, we have if-else statements - lets say we have 5 nodes & 1 ansible server
 - Not all nodes have same OS, RedHat uses yum and Ubuntu uses apt for installation
 - Another way: write 2 tasks that will be run on both nodes but only 1 will succeed & one will fail - bad practice
 - Use conditions for such different scenarios using the When statement. An example:
```
---
- hosts: demoByYash
  user: ansible
  become: yes
  tasks:
    - name: installing through yum for RedHat
      command: yum -y install chessx
      when: ansible_os_family == "RedHat"
    - name: installing through apt for Ubuntu
      command: apt install chessx
      when: ansible_os_family == "Debian"
...
```
- The above playbook would install Apache2 on the Debian Node using apt-while ignoring the RedHat nodes

## Vault
- Used for encrypting the playbooks and for security purposes using password
- You may not want people coming in and viewing the yaml so it can be encrypted with a password - if tried to be opened using the normal vi editor
- If you want to create an encrypted playbook, use the following command instead of `vi xyz.yaml`:
```
ansible-vault create xyz.yaml
```
- To edit the encrypted file, you won't be able to do it using vi so you'll use:
```
ansible-vault edit xyz.yaml
```
- To change the password of the vault, use:
```
ansible-vault rekey xyz.yaml
```
- To encrypt an existing playbook, run the follow commands:

```
ansible-vault encrypt existingPlaybook.yml
```
- To decrypt a playbook, run the following command
```
ansible-vault rekey xyz.yaml
```

## Roles
- When playbooks are made target, task, hand;er, conditions, vars,  sections are mentioned
- IRL tasks are many, when playbooks are too long its hard to understand what handler is dependent on what, what variable is being used where, etc.
- Roles solve this.
______________________________________________________________________________________
