# ad_auth

ansible.cfg:
---

[defaults]  
host_key_checking   = false  
inventory           = inventories/hosts  
private_key_file    = ~/.ssh/id_rsa  
remote_user         = ansible  
log_path            = logs  
vault_password_file = .ansible_vault_pass  


You should set 
- inventory
- private_key_file
- remote_user
- vault_password_file

vault_password_file shoud contain password for decrypt vars/passwd.yml (echo 'MyStrongVaulPassword' > .ansible_vault_pass)  
Create var/passwd.yml (echo 'ad_pass: StrongPassword' > var/passwd.yml)  
ansible-vault encrypt var/passwd.yml  
This file contains password of AD user with administrative rights.  

active_directory.yml:
---

- debug:                         true
- ad_server:  
    domain_name:                domain
    domain_controller_ip:        <ip>  
    domain_controller_fqdn:      <fqdn>  
    administrator_account:       <user>  
    administrator_password:      "{{ ad_pass }}"  
    allow_ssh_group:             <group>  
    
  
 Settings for active directory connection.  
 allow_ssh_group - group whith users which can connect over ssh.  
 debug  - for some denug information. May be set to false.
 
