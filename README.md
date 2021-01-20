# linux-user-creation

Hello, this repo is for creating multiusers for linux OS using Ansible.

## Prerequisits
- You will need to install Ansible on you system, please refer to this URL https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
- I used python 3 to encrypt the password to put it in the ansible playbook, to install python3 please refer to this URL https://computingforgeeks.com/generate-linux-user-encrypted-password-for-ansible/

## How to use:
- First, you will need to edit the hosts file which is located in `/etc/ansible/hosts` and add the IPs or hostnames of the servers you want to add users on like that for example:
```
[set-of-servers]
ip-1
ip-2
```
- Secondly, you need to set your usernames and passwords in this file `roles/user-creation/tasks/main.yml` in the `loop` section in the file.
- Subistitute the username you want to create with user1 and user2 and add more lines if you want to add more than 2 users.
- Please consider that the user password MUST be encrypted in order to put it in the file in that form.
- If you want to create a password, please use this command
```
python3 -c 'import crypt,getpass;pw=getpass.getpass();print(crypt.crypt(pw) if (pw==getpass.getpass("Confirm: ")) else exit())'
```
you will be prompted to enter a password you want and confirm it, then the encrypted password will be generated, copy it and paste it in the ansible-playbook after the username in the 'loop' section.
- Finally, you will need to change in the `configure.yml` file, the `hosts` parameter to match the group you created in the hosts file. Also you will need to change the `remote_user` paramter with the remote user you will use in the remote servers.
- Now you are ready to use the script using this command `ansible-playbook configure.yml`
 
