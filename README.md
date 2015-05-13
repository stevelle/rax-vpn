# Create a disposable L2TP over IPSec VPN hosted on Rackspace public cloud



based on https://gist.github.com/hwdsl2/9030462#file-vpnsetup-sh-L165

Requirements
---

- python 2.7x
- ansible
- pyrax

Instructions
---
1. environment must have a `RAX_CREDS_FILE` defined
2. modify the path in `playbooks/inventory/hosts` to include point to the path to your virtual environment interpretor, or omit the ansible_python_interpreter option completely if not using a virtual environment.
3. Generate the configuration file for the environment using Ansible Vault or just write a .yml file if you're feeling wild. See below for required parameters to do the needful.
4. Run the play to create the instance: `ansible-playbook -i playbooks/inventory/ -e @vpn_configuration_secrets.yml playbooks/setup.yml`
5. Run the play to setup the instance and configure the vpn: ``ansible-playbook -i playbooks/inventory/ -e @vpn_configuration_secrets.yml playbooks/secure.yml playbooks/vpn-libreswan-install.yml` 

The following is a template for the required parameters:
```yml
---
rax_name: as_instance_name
key_name: use_ssl_key_named
operator: username_to_ssh_with

vpn_username: as_vpn_username
vpn_password: as_vpn_password
vpn_shared_secret: and_pick_another_secret_key
```

