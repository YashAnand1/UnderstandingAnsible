
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
