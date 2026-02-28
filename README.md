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

### Appliance Image Checksum

Before running the playbook, you must supply the SHA256 checksum of the AWS Storage Gateway KVM appliance image. The checksum is used to verify the integrity of the downloaded file and will cause the playbook to fail if the download is corrupt or tampered with.

**How to obtain the checksum:**

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/storagegateway/)
2. Navigate to **Storage Gateway > Create Gateway**
3. Select **Amazon S3 File Gateway** as the gateway type
4. Select **Linux KVM** as the host platform
5. Click **Download Image** — the console displays the SHA256 checksum alongside the download link

**Where to set it:**

Open `provisioning/vars/sgw_kvm.yml` and replace `FIXME` with the checksum value from the console:

```yaml
aws_dl_checksum: "sha256:<paste-checksum-here>"
```

> **Note:** AWS periodically releases updated appliance images. When they do, the checksum will change. Update `aws_dl_checksum` to match the new value before re-running the playbook, otherwise the download verification step will fail.

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
