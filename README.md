# demo-ansible

This a demo showing the capabilities of Ansible. Using Vagrant two Virtualbox instance will be created with ansible installed on the 'master'. The 'minion' is configured so that the 'master' can access the 'minion. Through Ansible Gitlab will be installed with the correct external URL and a predefined root password. 

Please note that it is bad practice to push the vault_pass file. As this is a demo and not running in production, i feel comfortable enough to push it along with everything.

## Set-up 

```
git clone https://github.com/babutzc/demo-ansible.git
cd demo-ansible
mkdir keys 
ssh-keygen -f `pwd`/keys/id_rsa
vagrant up
```

## Enter the master 
```
vagrant ssh 
```

## enter the minion
```
vagrant ssh minion
```

## Run playbook on the master 
```
ansible-playbook playbooks/create.yml
```

## Use you're own key with ansible-vault. 

__Remove and create new file__
```
rm data/ansible/inventory/group_vars/gitlab.yml
vim data/ansible/inventory/group_vars/gitlab.yml
```

__data/ansible/inventory/group_vars/gitlab.yml__
```
version: 1 
external_url: <<your own URL>
initial_root_password: <<your own root password>>
```

__Encrypt__
```
ansible-vaut encrypt data/ansible/inventory/group_vars/gitlab.yml
```

__Create new vault_pass file__
```
echo "your ansible-vault password" > data/ansible/inventory/vault_pass
```
