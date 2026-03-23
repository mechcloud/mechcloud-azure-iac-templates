# MechCloud Azure IaC Templates

A curated collection of sample Infrastructure-as-Code (IaC) templates for provisioning Azure resources using [MechCloud's](https://mechcloud.io) stateless IaC engine.

## Overview

This repository contains ready-to-use MechCloud templates that demonstrate how to provision common Azure infrastructure patterns — from simple single-VM deployments to multi-tier architectures with load balancers, application gateways, and bastion hosts. Each template includes a scenario overview, an architecture diagram, a step-by-step walkthrough, and a complete unified YAML template.

These templates are designed to be used with [MechCloud's Stateless IaC](https://docs.mechcloud.io) feature, which allows you to define and deploy cloud infrastructure using a declarative YAML syntax without managing any state files.

## Key Features

- **Hierarchical resource nesting** — Define parent-child relationships naturally (e.g., Resource Group → VNet → Subnet → VM)
- **Dynamic macros** — Use built-in macros like `{{CURRENT_REGION}}`, `{{CURRENT_IP}}`, and `{{Image|arm64_ubuntu_24_04}}`
- **Cross-resource referencing** — Reference resources across the hierarchy using `ref:` syntax
- **No state management** — MechCloud handles state automatically; just define your desired infrastructure

## Getting Started

1. Sign up or log in at [MechCloud Portal](https://portal.mechcloud.io)
2. Connect your Azure subscription
3. Create a new stack and paste any template from this repository
4. Deploy and manage your infrastructure through MechCloud

## Templates

| Folder | Template | Description |
|--------|----------|-------------|
| **compute** | [public-web-vm-with-public-ip.md](templates/compute/public-web-vm-with-public-ip.md) | Public web application VM with a Static Public IP, VNet, Subnet, NSG, and Network Interface |
| | [private-vm-no-public-ip.md](templates/compute/private-vm-no-public-ip.md) | Private VM with no public IP, accessible only within the VNet |
| | [vm-with-managed-disk.md](templates/compute/vm-with-managed-disk.md) | VM with an additional managed data disk for separate application storage |
| **networking** | [multi-subnet-vnet.md](templates/networking/multi-subnet-vnet.md) | Two-tier VNet with public frontend subnet and private backend subnet with separate NSGs |
| | [vnet-peering.md](templates/networking/vnet-peering.md) | Two VNets peered together with bidirectional peering and VMs in each |
| | [nat-gateway-private-vm.md](templates/networking/nat-gateway-private-vm.md) | Private VM with outbound-only internet access via NAT Gateway (Standard_V2 SKU) |
| | [dns-zone-with-vm.md](templates/networking/dns-zone-with-vm.md) | VM with Azure DNS Zone and A record pointing to a Static Public IP |
| | [vnet-with-vpn-gateway.md](templates/networking/vnet-with-vpn-gateway.md) | VNet with VPN Gateway and site-to-site VPN connection to on-premises network |
| **load-balancing** | [vm-with-load-balancer.md](templates/load-balancing/vm-with-load-balancer.md) | VMs behind an Azure Standard Load Balancer with health probes and backend pool |
| | [vm-with-application-gateway.md](templates/load-balancing/vm-with-application-gateway.md) | VM behind an Azure Application Gateway (Standard_v2) with HTTP routing |
| | [vm-scale-set.md](templates/load-balancing/vm-scale-set.md) | VM Scale Set with CPU-based autoscaling (2–10 instances) and Standard Load Balancer |
| **storage** | [storage-account-with-blob-container.md](templates/storage/storage-account-with-blob-container.md) | Azure Storage Account with Blob Containers for application data and backups |
| **database** | [vm-with-azure-sql.md](templates/database/vm-with-azure-sql.md) | VM with Azure SQL Database (PaaS) for fully managed relational data |
| | [vm-with-redis-cache.md](templates/database/vm-with-redis-cache.md) | VM with Azure Cache for Redis for in-memory session and data caching |
| **security** | [bastion-host-secure-access.md](templates/security/bastion-host-secure-access.md) | VM accessible via Azure Bastion for secure SSH/RDP without public IP exposure |
| | [vm-with-key-vault.md](templates/security/vm-with-key-vault.md) | VM with Azure Key Vault for centralized secrets and key management |

## Contributing

Contributions are welcome! If you have a useful Azure infrastructure pattern, feel free to submit a pull request. Please follow the existing template structure which includes:

1. A descriptive title and introduction
2. A scenario overview with use case and key features
3. A Mermaid architecture diagram
4. Step-by-step YAML code blocks with explanations
5. A complete unified template at the end

## License

This project is licensed under the terms of the [LICENSE](LICENSE) file.
