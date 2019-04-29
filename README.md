# Deploy Multiple VMware VM with Ansible

## Description

Playbook and role to deploy multiple vSphere virtual machines from a template using Ansible. 

## Requirements
* Python (≥ 2.6)
* Ansible
* PyVmomi

## Configuration
The required files are:
```
├── ansible.cfg
├── answerfile.yml
├── deploy-kubernetes-prod.yml
├── roles
│   └── deploy-vsphere-template
│       └── tasks
│           └── main.yml
└── vms-to-deploy
```

1. Edit the ```vms-to-deploy``` file to define the number of virtual machines you want to deploy, as well as their names, datastore, IP and notes.
2. Edit the ```vm-size/{{size}}.yml``` file(s) to set the correct parameter for
    * the infrastructure (where to deploy)
    * the common options for the virtual machines
    Or make a new environment from the `vars/environment/_template.yaml` file, replacing placeholders with correct values. Then encrypt the newly created file with `ansible-vault encrypt vars/environment/my_new_env.yaml`
3. (optional) Edit the role.

## Execution

```
ansible-playbook -i vms-to-deploy.ini deploy-kubernetes-prod.yml --vault-id @prompt
```

### Decommission
The following will *delete* VMs listed in the inventory:

```
ansible-playbook -i vms-to-deploy.ini decom-kubernetes-prod.yml --vault-id @prompt
```

