# Virtualization
This all needs to be re-worked because I wrote this up last month before VMWare modified the VMUG Advantage benefits to no longer provide 365 EvalExperience licenses.

Its got soome of the basics that didn't change with the move to Proxmox though.


## Architecture
There are two primary enclaves, one is a physical enclave hosting all the core defensive controls, and the other is a virtual enclave that we'll use as our range.

| Enclave Name    | Use Case |
| -------- | ------- |
| BLUENET  | Core architecture hosting enterprise services, defensive mitigations, etc.    |
| RANGENET | Nested virtualization, cyber range for detonation, sandboxing, and pentesting.     |

BLUENET is the core compute powerhouse, and hosts RANGENET using nested virtualization. BLUENET consists of two resouorce groups

| Cluster Name | Use Case |
| -------- | ------- |
| CORE  | Primary compute, hosts compute-heavy resources, Splunk, virtualization for RANGENET    |
| MINI | Core services. Hosts Active Directory, ADCS, Duo, and other core services that enable the lab.     |


### BLUENET Hosts

| Host Name | Model | CPU | RAM | Storage | Network |
| --------- | ----- | --- | --- | ------- | ------- |
| VIRT01 | Dell Poweredge R630 | 2 x E5-2680 v3 @ 2.50GHz (24 Cores/48 Threads) | 192GB | 1x800Gb SAS, 15TB iSCSI Datastore | 4x1Gb, 2x10Gb, 1xIPMI |
| VIRT02 | Dell Poweredge R630 | 2 x E5-2680 v3 @ 2.50GHz (24 Cores/48 Threads) | 192GB | 1x800Gb SAS, 15TB iSCSI Datastore | 4x1Gb, 2x10Gb, 1xIPMI |
| VIRT01-MINI | HP ProDesk 600 G5 Mini | 1 x i5-9500T @ 2.20Ghz (6 Cores/6 Threads) | 48GB | 1x4TB NVME, 15TB iSCSI Datastore | 1x1Gb |
| VIRT02-MINI | HP ProDesk 600 G5 Mini | 1 x i5-9500T @ 2.20Ghz (6 Cores/6 Threads) | 48GB | 1x4TB NVME, 15TB iSCSI Datastore | 1x1Gb |


### Proxmox Authentication
Proxmox is configured to use OIDC through Cisco Duo to provide SSO

This is documented over on: [Blog - Duo SSO for Proxmox](../blog/posts/proxmox-duo-sso.md)

#### Authorized Groups
Only certain groups are authorized to login to Proxmox.

| Group Name | Permissions | Proxmox Role |
| ---------- | ----------- | ------------ |
| duo-oidc\Proxmox Super Admins | Full Administrator Permissions | Administrator |


## Time Synchronization
Time synchronization with the host is turned off on all hosts. This ensures that skews in the hardware clock dont result in VMs receiving incorrect times.

Times are synced with trusted NTP sources.

### Trusted NTP Servers

| NTP Server Address | Role | Port | Auth |
| ------------------ | ---- | ---- | ---- |
| 0.us.pool.ntp.org | Primary | udp/123 | No Auth |
| 1.us.pool.ntp.org | Secondary | udp/123 | No Auth |
| 2.us.pool.ntp.org | Tertiary | udp/123 | No Auth | 
| 3.us.pool.ntp.org | Last Resort | udp/123 | No Auth |

#### Standard STIG-like logon message
We do have a standard STIG-like logo message for just about every system in our environment. It's minimal and a check-in the box just to give us a more enterprise-feely environment.

```text
    This device is intended for authorized use only. Unauthorized access to this system is prohibited. 
    The system is monitored for security, compliance, and adherence to security policies.
```