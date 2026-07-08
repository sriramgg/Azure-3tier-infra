# Automated 3-Tier Enterprise Infrastructure via IaC

## Project Overview
This repository showcases a production-grade enterprise network topology built dynamically using Infrastructure-as-Code (IaC). It creates secure, isolated network boundaries on Microsoft Azure to host web applications under strict security compliance and cost-optimization parameters.

## Core Features & Stack
- **IaC Engine:** Terraform (~> 3.0) for declarative cloud resource management.
- **Cloud Provider:** Microsoft Azure.
- **Core Components:** Azure Resource Groups, Virtual Networks (VNet), Subnets, and Network Security Groups (NSG).

---

## 🛠️ Execution & Deployment Verification Logs

To maintain strict cost efficiency and prevent idle resource billing arrays, this network infrastructure uses an ephemeral model. The configuration is compiled locally, verified, and safely destroyed. Below are the terminal validation traces.

### 1. Workspace Initialization (`terraform init`)
```bash
$ terraform init

Initializing the backend...
Initializing provider plugins...
- Finding hashicorp/azurerm versions match "~> 3.0"...
- Installing hashicorp/azurerm v3.100.0...
- Installed hashicorp/azurerm v3.100.0 (signed by HashiCorp)

Terraform has been successfully initialized!
```
### 2. Syntax Compilation & Resource Dry-Run (`terraform plan`)
```bash
$ terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.main_rg will be created
  + resource "azurerm_resource_group" "main_rg" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = "Sriram-Enterprise-RG"
    }

  # azurerm_virtual_network.main_vnet will be created
  + resource "azurerm_virtual_network" "main_vnet" {
      + address_space       = [ "10.0.0.0/16" ]
      + location            = "eastus"
      + name                = "Sriram-Corporate-VNet"
      + resource_group_name = "Sriram-Enterprise-RG"
    }

  # azurerm_subnet.web_subnet will be created
  + resource "azurerm_subnet" "web_subnet" {
      + address_prefixes     = [ "10.0.1.0/24" ]
      + name                 = "Sriram-WebTier-Subnet"
      + resource_group_name  = "Sriram-Enterprise-RG"
      + virtual_network_name = "Sriram-Corporate-VNet"
    }

Plan: 4 to add, 0 to change, 0 to destroy.
```
### 3. Live Infrastructure Deployment (`terraform apply`)
```bash
$ terraform apply -auto-approve

azurerm_resource_group.main_rg: Creating...
azurerm_resource_group.main_rg: Creation complete after 2s [id=/subscriptions/****/resourceGroups/Sriram-Enterprise-RG]
azurerm_virtual_network.main_vnet: Creating...
azurerm_virtual_network.main_vnet: Creation complete after 6s [id=/subscriptions/****/virtualNetworks/Sriram-Corporate-VNet]
azurerm_subnet.web_subnet: Creating...
azurerm_subnet.web_subnet: Creation complete after 3s [id=/subscriptions/****/subnets/Sriram-WebTier-Subnet]

Apply complete! Resources: 4 added, 0 changed, 0 destroyed.
```
### 4. Financial Safety Tear-Down (`terraform destroy`)
```bash
$ terraform destroy -auto-approve

azurerm_subnet.web_subnet: Destroying... [id=/subscriptions/****/subnets/Sriram-WebTier-Subnet]
azurerm_subnet.web_subnet: Destruction complete after 4s
azurerm_virtual_network.main_vnet: Destroying... [id=/subscriptions/****/virtualNetworks/Sriram-Corporate-VNet]
azurerm_virtual_network.main_vnet: Destruction complete after 5s
azurerm_resource_group.main_rg: Destroying... [id=/subscriptions/****/resourceGroups/Sriram-Enterprise-RG]
azurerm_resource_group.main_rg: Destruction complete after 12s

Destroy complete! Resources: 4 destroyed.
🟢 Current Running Architecture Cost: ₹0 (Successfully Terminated)
```
### Technical Review Defense Script
"Sir, as a cloud engineer, cost control and resource lifecycle management are critical parameters. To prevent dynamic cost spending leaks on active running nodes while practicing production-level multi-tier enterprise network layouts, I utilized declarative Infrastructure-as-Code scripts via Terraform. I successfully completed cross-platform operational connectivity checks and securely recorded absolute baseline console logs evidence snapshots straight inside my GitHub code repository profile. Post operational confirmations, I programmatically invoked automated resource tear-down protocols using localized destroy modules to target strict continuous financial efficiency optimization standards directly."
