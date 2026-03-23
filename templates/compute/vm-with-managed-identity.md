# Deploy a VM with System-Assigned Managed Identity on Azure

This guide demonstrates how to use MechCloud's stateless IaC to provision a VM with a system-assigned managed identity for passwordless authentication to Azure services.

## Scenario Overview
**Use Case:** A VM that authenticates to Azure services (Key Vault, Storage, SQL) without storing credentials — eliminating the need for service principals, passwords, or connection strings in application code.
**Key MechCloud Features Highlighted:**
- Hierarchical resource nesting (Resource Group → VNet → Subnet → VM)
- Cross-resource referencing (`ref:`)
- Managed identity and role assignment in a single template

### Architecture Diagram

```mermaid
flowchart TB
    subgraph RG [Resource Group: rg1]
        VM(VM: app-vm<br/>Managed Identity) -->|Passwordless| KV[Key Vault]
        VM -->|Passwordless| Storage[(Storage Account)]
        Role[Role Assignment: Reader]
    end
```

***

### Complete Unified Template

```yaml
resources:
  - type: Microsoft.Resources/resourceGroups
    name: rg1
    location: "{{CURRENT_REGION}}"
    resources:
      - type: Microsoft.Network/virtualNetworks
        name: vnet1
        props:
          properties:
            addressSpace:
              addressPrefixes:
                - "10.0.0.0/16"
          resources:
            - type: Microsoft.Network/virtualNetworks/subnets
              name: subnet1
              props:
                properties:
                  addressPrefix: "10.0.1.0/24"

      - type: Microsoft.Network/networkSecurityGroups
        name: nsg1
        props:
          properties:
            securityRules:
              - name: allow-ssh
                properties:
                  priority: 100
                  direction: Inbound
                  access: Allow
                  protocol: Tcp
                  sourceAddressPrefix: "{{CURRENT_IP}}/32"
                  sourcePortRange: "*"
                  destinationAddressPrefix: "*"
                  destinationPortRange: "22"

      - type: Microsoft.Network/networkInterfaces
        name: nic1
        props:
          properties:
            ipConfigurations:
              - name: ipconfig1
                properties:
                  subnet:
                    id: "ref:rg1/vnet1/subnet1"
                  privateIPAllocationMethod: Dynamic
            networkSecurityGroup:
              id: "ref:rg1/nsg1"

      - type: Microsoft.Compute/virtualMachines
        name: app-vm
        props:
          identity:
            type: SystemAssigned
          properties:
            hardwareProfile:
              vmSize: Standard_B2ps_v2
            osProfile:
              computerName: app-vm
              adminUsername: azureuser
              linuxConfiguration:
                disablePasswordAuthentication: true
                ssh:
                  publicKeys:
                    - path: /home/azureuser/.ssh/authorized_keys
                      keyData: "ssh-rsa AAAA...your-key"
            storageProfile:
              imageReference:
                publisher: Canonical
                offer: ubuntu-24_04-lts
                sku: server-arm64
                version: latest
              osDisk:
                createOption: FromImage
                managedDisk:
                  storageAccountType: Premium_LRS
            networkProfile:
              networkInterfaces:
                - id: "ref:rg1/nic1"

      - type: Microsoft.Storage/storageAccounts
        name: mcidentitystorage1
        props:
          kind: StorageV2
          sku:
            name: Standard_LRS

      - type: Microsoft.Authorization/roleAssignments
        name: vm-storage-reader
        props:
          scope: "ref:rg1/mcidentitystorage1"
          properties:
            roleDefinitionId: "2a2b9908-6ea1-4ae2-8e65-a410df84e7d1"
            principalId: "ref:rg1/app-vm.identity.principalId"
            principalType: ServicePrincipal
```
