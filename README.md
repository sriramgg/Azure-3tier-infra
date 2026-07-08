# Automated 3-Tier Enterprise Infrastructure via IaC

[![Terraform](https://img.shields.io/badge/IaC-Terraform-7B42BC?logo=terraform)](https://www.terraform.io)
[![Azure](https://img.shields.io/badge/Cloud-Azure-0078D4?logo=microsoftazure)](https://azure.microsoft.com)
[![License](https://img.shields.io/badge/License-MIT-green)](#)

A production-grade, fully isolated **3-tier network topology** on Microsoft Azure, provisioned entirely through declarative Infrastructure-as-Code using Terraform.

---

## Skills Demonstrated

`Terraform` `Azure Networking` `Infrastructure-as-Code` `Network Security` `Subnet Isolation` `NSG Rules` `Cloud Architecture` `Cost Optimization`

---

## Architecture

```
10.0.0.0/16 ─── Sriram-Corporate-VNet
 ├── 10.0.1.0/24 ── Sriram-WebTier-Subnet   (HTTP :80 from Internet)
 ├── 10.0.2.0/24 ── Sriram-AppTier-Subnet    (App :8080 from Web tier only)
 └── 10.0.3.0/24 ── Sriram-DataTier-Subnet   (SQL :1433 from App tier only)
```

Each tier is isolated with its own **Network Security Group** enforcing least-privilege ingress:
- **Web** — accepts public HTTP traffic
- **App** — accepts traffic only from Web subnet
- **Data** — accepts traffic only from App subnet

---

## Provisioned Resources

| Resource | Name | Purpose |
|----------|------|---------|
| Resource Group | `Sriram-Enterprise-RG` | Logical container for all resources |
| Virtual Network | `Sriram-Corporate-VNet` | Isolated network space (`10.0.0.0/16`) |
| Subnet | `Sriram-WebTier-Subnet` | Public-facing web layer |
| Subnet | `Sriram-AppTier-Subnet` | Business logic layer |
| Subnet | `Sriram-DataTier-Subnet` | Database layer |
| NSG | `Sriram-WebTier-NSG` | Allows HTTP :80 inbound |
| NSG | `Sriram-AppTier-NSG` | Allows :8080 from Web tier |
| NSG | `Sriram-DataTier-NSG` | Allows :1433 from App tier |
| NSG Association | Web/App/Data | Attaches each NSG to its subnet |

---

## Quick Start

```bash
# Clone the repository
git clone https://github.com/sriramgg/Azure-3tier-infra.git
cd Azure-3tier-infra

# Initialize Terraform
terraform init

# Preview resources to be created
terraform plan

# Deploy (requires Azure credentials)
terraform apply -auto-approve

# Teardown when done
terraform destroy -auto-approve
```

---

## Cost Optimization Strategy

All infrastructure follows an **ephemeral lifecycle model**. Resources are provisioned on demand for validation, captured in verified terminal logs, and immediately destroyed. This maintains full operational proof without incurring idle cloud billing.

---

## Prerequisites

- Terraform >= 1.3
- Azure subscription with valid credentials
- Azure CLI authenticated (`az login`)

---

## License

MIT
