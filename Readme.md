# Deploy / Destroy a VMware vSphere three tier app using Ansible

### Configuration
```
├── ansible.cfg
├── deploy.yml
├── destroy.yml
├── helpers
│   ├── check_datastore_free_space.yml
│   ├── create_folders.yml
│   ├── create_tags.yml
│   ├── remove_folders.yml
│   └── remove_tags.yml
├── host_vars
│   ├── nat-app01
│   ├── nat-db01
│   └── nat-web01
├── Readme_gpg.md
├── Readme.md
├── roles
│   ├── check-datastore-free-space
│   │   └── tasks
│   │       └── main.yml
│   ├── deploy-vm
│   │   └── tasks
│   │       └── main.yml
│   └── destroy-vm
│       └── tasks
│           └── main.yaml
└── three-tier-app
```

File Name: three-tier-app - Inventory file

File Name: deploy.yml - Deploy three-tier-app VMs from template.

File Name: destroy.yml - Power OFF and Remove three-tier-app VMs.

### Roles & Tasks

File Name: roles/check-datastore-free-space/tasks/main.yml - Display datastore usage. Fails if datastore usage exceeds 90%.

File Name: roles/deploy-vm/tasks/main.yml - Deploy a new VM from a template.

File Name: roles/destroy-vm/tasks/main.yml - Power OFF and Remove an existing VM.

### Helpers

File Name: helpers/create_tags.yml - Create a VMware category and VM tag.

File Name: helpers/create_folders.yml - Create a VM folder and sub folder on given datacenter.

### Requirements

1. Variables vsphere_tag_category and vsphere_tag must exist
   To create the category and tag execute: cd helpers  &&  ansible-playbook create_tags.yml

2. Variables deploy_vsphere_folder and deploy_vsphere_sub_folder must exist
   To create vSphere folder and sub-folder execute: cd helpers && ansible-playbook create_folders.yml

### Execution

To deploy a new VM first create the VM configuration file and place the configuration file in host_vars directory.

### Deploy three-tier-app VMs from template.

    Check Mode (Dry Run)

    \> ansible-playbook -C deploy.yml

    Execute

    \> ansible-playbook deploy.yml 

### Power OFF and Remove three-tier-app VMs.

    Check Mode (Dry Run)

    \> ansible-playbook -C destroy.yml

    Execute

    \> ansible-playbook remove.yml


### Encrypting a string using GPG and Pass

If the vCenter credentials are managed via GPG and Pass, set the apropiate environment variables

    export TF_VAR_provider_vsphere_host=$(pass provider_vsphere_host)

    export TF_VAR_provider_vsphere_user=$(pass provider_vsphere_user)

    export TF_VAR_provider_vsphere_password=$(pass provider_vsphere_password)
