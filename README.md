# Windows Server Administration Labs

**Ankita Srivastava | Windows Server • Active Directory • Azure**

This repository documents my hands-on Windows Server administration practice. The current labs follow one environment from Azure infrastructure and Windows Server VM deployment through Active Directory Domain Services installation and promotion of the first domain controller.

I documented my lab steps and configuration with screenshots from my environment.

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

## Skills demonstrated so far

- Azure resource groups, virtual networks, subnets, and Windows Server VM deployment
- Windows Server 2025 administration
- Server Manager and Add Roles and Features
- Active Directory Domain Services
- New forest and root-domain creation
- DNS Server and Global Catalog configuration
- NTDS and SYSVOL path configuration
- Domain-controller promotion and post-promotion verification

More Windows Server administration labs will be added as the environment develops.
