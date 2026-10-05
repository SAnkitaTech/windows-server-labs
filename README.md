# Windows Server Administration Labs

**Ankita Srivastava | Windows Server • Active Directory • Azure**

This repository documents my hands-on Windows Server administration practice. The current labs follow one environment from Azure infrastructure and Windows Server VM deployment through domain-controller promotion, OU organization, basic Group Policy, and shared-folder permissions.

## Current lab environment

| Component | Configuration |
| --- | --- |
| Azure resource group | `PS-Ankita` |
| Azure virtual network | `myvnet` |
| Subnet | `snet-centralindia-2` — `10.0.1.0/24` |
| Windows Server VM | `AnkitaDC1` |
| Region | Central India |
| VM image | Windows Server 2025 Datacenter: Azure Edition - x64 Gen2 |
| VM size | `Standard_B2s_v2` — 2 vCPUs, 8 GiB RAM |
| Active Directory forest/domain | `ankita.com` |
| NetBIOS name | `ANKITA` |
| First domain controller | `AnkitaDC1` |

## Labs

### 01 — Azure Windows Server VM Deployment
Provision a Windows Server 2025 virtual machine in Azure, including the resource group, VNet/subnet selection, VM sizing, NIC/network security settings, public IP creation, and deployment verification.

[Open the lab](01-azure-windows-server-vm/README.md)

### 02 — Active Directory Domain Controller
Prepare the Windows Server VM, install Active Directory Domain Services, create the `ankita.com` forest, and promote `AnkitaDC1` to the first domain controller with DNS and Global Catalog.

[Open the lab](02-active-directory-domain-controller/README.md)

### 03 — Active Directory OUs and Basic Group Policy
Organize users and computers into OUs, pre-stage computer accounts, and configure Control Panel and removable storage policies.

[Open the lab](03-active-directory-ou-and-group-policy/README.md)

### 04 — NTFS and Share Permissions
Configure a shared folder, manage IT Team access, convert permission inheritance, and review Effective Access and advanced NTFS permissions.

[Open the lab](04-ntfs-and-share-permissions/README.md)

### 05 — Group Policy Administration
Configure and verify policies in the Windows Server lab.

[Windows Defender Firewall: Domain Profile](05-group-policy/windows-defender-firewall/README.md)

## Skills demonstrated so far

- Azure resource groups, virtual networks, subnets, and Windows Server VM deployment
- SMB shares, NTFS permissions, inheritance, and Effective Access
- Group Policy creation, domain linking, and Windows Defender Firewall policy verification
- Windows Server 2025 administration
- Server Manager and Add Roles and Features
- Active Directory Domain Services
- New forest and root-domain creation
- DNS Server and Global Catalog configuration
- NTDS and SYSVOL path configuration
- Domain-controller promotion and post-promotion verification

More Windows Server administration labs will be added as the environment develops.
