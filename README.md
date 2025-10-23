# Ansible Playbooks for AWS Storage Gateway on RHEL9

Ansible playbooks to deploy multiple AWS Storage Gateway File Gateway appliances on RHEL9/KVM. Supports AWS Commercial partition.

## Prerequisites

- RHEL 9 host with KVM support
- Ansible 2.9 or higher
- AWS account with appropriate permissions
- Sufficient disk space for VM images and virtual disks

## Usage

### Deploy Storage Gateway

```bash
ansible-playbook -i inventory site.yml
```

### Configuration

Edit your inventory file and configure the storage gateway appliances according to your requirements. Adjust hardware specifications (CPU, memory, disk sizes) as needed.

## Integration Testing

### Prerequisites

- Vagrant 2.4.3
- VirtualBox 6.1

### Running Tests

```bash
vagrant up
```

### Sample Test Output

The test suite performs the following operations:

1. **Install KVM** - Installs required KVM packages and enables libvirtd
2. **Download VM Templates** - Downloads AWS Storage Gateway appliance templates
3. **Provision Virtual Disks** - Creates primary and cache disks for each gateway
4. **Initialize Appliances** - Deploys and configures Storage Gateway VMs

Example successful run:
```
PLAY RECAP *********************************************************************
kvmhost                    : ok=9    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## Authors
- [Erin L. Kolp](https://github.com/erinlkolp)
