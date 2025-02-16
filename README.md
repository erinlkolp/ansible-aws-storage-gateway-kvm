## Ansible Playbooks for AWS Storage Gateway on RHEL9

Playbooks to deploy multiple AWS Storage Gateway File Gateway appliances on RHEL9/KVM. Supports AWS Commercial partition. Full Readme coming soon!

### Usage

```bash
ansible here
```

### Integration Testing

##### Pre-requisites

- Vagrant 2.4.3
- VirtualBox 6.1

##### Running Tests

```bash
vagrant up
```

##### Sample Test Output

```bash
</SNIP!>
PLAY [Install KVM] *************************************************************

TASK [Gathering Facts] *********************************************************
ok: [kvmhost]

TASK [Install KVM Base System] *************************************************
changed: [kvmhost] => (item=qemu-kvm-core)
changed: [kvmhost] => (item=qemu-kvm-tools)
changed: [kvmhost] => (item=libvirt)
changed: [kvmhost] => (item=virt-manager)
changed: [kvmhost] => (item=virt-install)
changed: [kvmhost] => (item=virt-viewer)
changed: [kvmhost] => (item=virt-top)
changed: [kvmhost] => (item=libguestfs-tools)
ok: [kvmhost] => (item=libvirt-daemon-config-network)
changed: [kvmhost] => (item=unzip)

TASK [Enable and Start Libvirtd] ***********************************************
changed: [kvmhost]

PLAY [Download VM Templates from AWS] ******************************************

TASK [Gathering Facts] *********************************************************
ok: [kvmhost]

TASK [Create Landing Dir] ******************************************************
changed: [kvmhost]

TASK [Download AWS GovCloud SG Appliance Template] *****************************
changed: [kvmhost]

TASK [Download AWS Commercial SG Appliance Template] ***************************
changed: [kvmhost]

TASK [Create AWS GovCloud Archive Target Dir] **********************************
changed: [kvmhost]

TASK [Create AWS Commercial Archive Target Dir] ********************************
changed: [kvmhost]

TASK [Extract AWS GovCloud Base Image] *****************************************
changed: [kvmhost]

TASK [Extract AWS Commercial Base Image] ***************************************
changed: [kvmhost]

PLAY RECAP *********************************************************************
kvmhost                    : ok=22   changed=10   unreachable=0    failed=0    skipped=4    rescued=0    ignored=0   

==> kvmhost: Running provisioner: ansible...
    kvmhost: Running ansible-playbook...

PLAY [all] *********************************************************************

TASK [Gathering Facts] *********************************************************
[WARNING]: Platform linux on host kvmhost is using the discovered Python
interpreter at /usr/bin/python3.9, but future installation of another Python
interpreter could change the meaning of that path. See
https://docs.ansible.com/ansible-
core/2.18/reference_appendices/interpreter_discovery.html for more information.
ok: [kvmhost]

TASK [Check Prereqs] ***********************************************************
ok: [kvmhost]

TASK [Get VM List] *************************************************************
ok: [kvmhost]

PLAY [all] *********************************************************************

TASK [Gathering Facts] *********************************************************
ok: [kvmhost]

TASK [Create Live VM Disk Target Dir] ******************************************
changed: [kvmhost]

TASK [Provision AWS Commercial Virtual Disks] **********************************
changed: [kvmhost] => (item={'key': 'devcomm-sgw', 'value': {'hardware': {'cpu_allocation': 2, 'mem_allocation': 6000, 'primary_disk': 80, 'cache_disk': 40}}})

TASK [Initialize AWS Commercial Storage Gateway Appliances] ********************
changed: [kvmhost] => (item={'key': 'devcomm-sgw', 'value': {'hardware': {'cpu_allocation': 2, 'mem_allocation': 6000, 'primary_disk': 80, 'cache_disk': 40}}})

PLAY RECAP *********************************************************************
kvmhost                    : ok=9    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

## Authors
- [Erin L. Kolp](https://github.com/erinlkolp)
