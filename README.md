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
| **cdn** | [azure-cdn-static-site.md](templates/cdn/azure-cdn-static-site.md) | Azure CDN with Storage Account static website for global content delivery |
| **compute** | [public-web-vm-with-public-ip.md](templates/compute/public-web-vm-with-public-ip.md) | Public web application VM with a Static Public IP, VNet, Subnet, NSG, and Network Interface |
| | [private-vm-no-public-ip.md](templates/compute/private-vm-no-public-ip.md) | Private VM with no public IP, accessible only within the VNet |
| | [vm-with-managed-disk.md](templates/compute/vm-with-managed-disk.md) | VM with an additional managed data disk for separate application storage |
| | [vm-with-managed-identity.md](templates/compute/vm-with-managed-identity.md) | VM with system-assigned managed identity for passwordless Azure service access |
| | [vm-with-custom-script.md](templates/compute/vm-with-custom-script.md) | VM with Custom Script Extension for automated software installation |
| | [vm-scale-set-custom-image.md](templates/compute/vm-scale-set-custom-image.md) | VM Scale Set with autoscaler and rolling upgrade policy |
| | [vm-availability-zones.md](templates/compute/vm-availability-zones.md) | VMs across availability zones with zone-redundant load balancer for HA |
| | [app-service-with-sql.md](templates/compute/app-service-with-sql.md) | App Service (Web App) with Azure SQL Database backend |
| | [app-service-deployment-slots.md](templates/compute/app-service-deployment-slots.md) | App Service with staging deployment slots for zero-downtime deployments |
| | [batch-account.md](templates/compute/batch-account.md) | Azure Batch account with pools for large-scale parallel computing |
| **containers** | [aci-container-group.md](templates/containers/aci-container-group.md) | Azure Container Instances (ACI) container group for serverless containers |
| | [acr-registry.md](templates/containers/acr-registry.md) | Azure Container Registry with geo-replication and webhook |
| | [aks-cluster.md](templates/containers/aks-cluster.md) | AKS cluster with managed node pool for Kubernetes workloads |
| **database** | [vm-with-azure-sql.md](templates/database/vm-with-azure-sql.md) | VM with Azure SQL Database (PaaS) for fully managed relational data |
| | [vm-with-redis-cache.md](templates/database/vm-with-redis-cache.md) | VM with Azure Cache for Redis for in-memory session and data caching |
| | [cosmos-db.md](templates/database/cosmos-db.md) | Azure Cosmos DB with multiple containers for globally distributed NoSQL |
| | [azure-sql-elastic-pool.md](templates/database/azure-sql-elastic-pool.md) | Azure SQL Elastic Pool with multiple tenant databases for SaaS |
| | [postgresql-flexible-server.md](templates/database/postgresql-flexible-server.md) | Azure Database for PostgreSQL Flexible Server with VNet integration |
| | [mysql-flexible-server.md](templates/database/mysql-flexible-server.md) | Azure Database for MySQL Flexible Server with high availability |
| **load-balancing** | [vm-with-load-balancer.md](templates/load-balancing/vm-with-load-balancer.md) | VMs behind an Azure Standard Load Balancer with health probes and backend pool |
| | [vm-with-application-gateway.md](templates/load-balancing/vm-with-application-gateway.md) | VM behind an Azure Application Gateway (Standard_v2) with HTTP routing |
| | [vm-scale-set.md](templates/load-balancing/vm-scale-set.md) | VM Scale Set with CPU-based autoscaling (2–10 instances) and Standard Load Balancer |
| **messaging** | [event-hub.md](templates/messaging/event-hub.md) | Azure Event Hubs for high-throughput real-time data streaming with capture |
| | [service-bus.md](templates/messaging/service-bus.md) | Azure Service Bus with queues, topics, and subscriptions for enterprise messaging |
| **monitoring** | [log-analytics-workspace.md](templates/monitoring/log-analytics-workspace.md) | Log Analytics Workspace with diagnostic settings for centralized monitoring |
| | [azure-monitor-alerts.md](templates/monitoring/azure-monitor-alerts.md) | Azure Monitor metric alerts with action groups for proactive VM monitoring |
| **networking** | [multi-subnet-vnet.md](templates/networking/multi-subnet-vnet.md) | Two-tier VNet with public frontend subnet and private backend subnet with separate NSGs |
| | [vnet-peering.md](templates/networking/vnet-peering.md) | Two VNets peered together with bidirectional peering and VMs in each |
| | [nat-gateway-private-vm.md](templates/networking/nat-gateway-private-vm.md) | Private VM with outbound-only internet access via NAT Gateway (Standard_V2 SKU) |
| | [dns-zone-with-vm.md](templates/networking/dns-zone-with-vm.md) | VM with Azure DNS Zone and A record pointing to a Static Public IP |
| | [vnet-with-vpn-gateway.md](templates/networking/vnet-with-vpn-gateway.md) | VNet with VPN Gateway and site-to-site VPN connection to on-premises network |
| | [vnet-with-firewall.md](templates/networking/vnet-with-firewall.md) | VNet with Azure Firewall for centralized traffic inspection |
| | [private-endpoint.md](templates/networking/private-endpoint.md) | Private Endpoints for secure private access to Azure services |
| | [front-door.md](templates/networking/front-door.md) | Azure Front Door for global HTTP load balancing with edge caching |
| | [traffic-manager.md](templates/networking/traffic-manager.md) | Azure Traffic Manager for DNS-based multi-region load balancing |
| | [express-route.md](templates/networking/express-route.md) | ExpressRoute circuit with VNet Gateway for dedicated private connectivity |
| | [vnet-hub-spoke.md](templates/networking/vnet-hub-spoke.md) | Hub-and-spoke VNet topology with shared services and workload isolation |
| **security** | [bastion-host-secure-access.md](templates/security/bastion-host-secure-access.md) | VM accessible via Azure Bastion for secure SSH/RDP without public IP exposure |
| | [vm-with-key-vault.md](templates/security/vm-with-key-vault.md) | VM with Azure Key Vault for centralized secrets and key management |
| | [key-vault-secrets.md](templates/security/key-vault-secrets.md) | Azure Key Vault with secrets and access policies |
| | [waf-with-app-gateway.md](templates/security/waf-with-app-gateway.md) | WAF with Application Gateway for OWASP threat protection |
| | [defender-for-cloud.md](templates/security/defender-for-cloud.md) | Microsoft Defender for Cloud with security contacts and auto-provisioning |
| | [policy-assignment.md](templates/security/policy-assignment.md) | Azure Policy assignments for governance and compliance enforcement |
| **serverless** | [function-app-http.md](templates/serverless/function-app-http.md) | Azure Function App with HTTP trigger for serverless API endpoints |
| | [function-app-queue-trigger.md](templates/serverless/function-app-queue-trigger.md) | Azure Function App with Queue Storage trigger for event-driven processing |
| **storage** | [storage-account-with-blob-container.md](templates/storage/storage-account-with-blob-container.md) | Azure Storage Account with Blob Containers for application data and backups |
| | [blob-lifecycle-management.md](templates/storage/blob-lifecycle-management.md) | Storage Account with lifecycle policies for automated tier transitions |
| | [azure-files-share.md](templates/storage/azure-files-share.md) | Azure Files share with private endpoint for secure SMB access |
| | [data-lake-gen2.md](templates/storage/data-lake-gen2.md) | Azure Data Lake Storage Gen2 with hierarchical namespace for big data |

## Contributing

Contributions are welcome! If you have a useful Azure infrastructure pattern, feel free to submit a pull request. Please follow the existing template structure which includes:

1. A descriptive title and introduction
2. A scenario overview with use case and key features
3. A Mermaid architecture diagram
4. Step-by-step YAML code blocks with explanations
5. A complete unified template at the end

## License

This project is licensed under the terms of the [LICENSE](LICENSE) file.
