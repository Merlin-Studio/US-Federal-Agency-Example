# acme-lza1 - Configuration Documentation

> **Generated:** 2026-03-11T10:26:11.613782Z
> **Profile:** Advanced
> **Organization:** acme.com

---

## Executive Summary

This document describes the Cloud Foundation configuration for **acme.com**. This establishes your GCP Landing Zone.

| Attribute | Value |
|-----------|-------|
| Cloud Foundation Name | `acme-lza1` |
| Organization ID | `593874125053` |
| Primary Region | `us-central1` |
| Configuration Profile | Advanced |
| Architecture Type | Hub and Spoke |

| Compliance Frameworks | SOC2, FEDRAMP, NIST, SOX |


| Organization Policies | 15 enforced |


| Log Retention | 2555 days |

| Billing Account | `013478-95D694-5670A9` |


### Compliance Requirements

This cloud foundation is configured to support:

- **SOC2**

- **FEDRAMP**

- **NIST**

- **SOX**



---

## 1. Organization Structure

### 1.1 Folder Hierarchy


```
acme.com (593874125053)
│

├── 📁 Production
│   └── Purpose: environment

├── 📁 Staging
│   └── Purpose: environment

├── 📁 Development
│   └── Purpose: environment

├── 📁 Shared Services
│   └── Purpose: shared_services

├── 📁 Security
│   └── Purpose: security

├── 📁 Networking
│   └── Purpose: networking

├── 📁 Data Platform
│   └── Purpose: data

├── 📁 Sandbox
│   └── Purpose: sandbox

```

| Folder | Purpose | Description |
|--------|---------|-------------|

| Production | environment | Production workloads |

| Staging | environment | Pre-production testing |

| Development | environment | Development |

| Shared Services | shared_services | Common infrastructure |

| Security | security | Security tooling |

| Networking | networking | Hub networks and connectivity |

| Data Platform | data | Analytics and data services |

| Sandbox | sandbox | Experimentation |



### 1.2 Bootstrap Projects


| Project Name | Folder | Purpose | APIs |
|--------------|--------|---------|------|

| `prj-new-service` | Shared Services | cicd | cloudbuild.googleapis.com, cloudkms.googleapis.com, secretmanager.googleapis.com, logging.googleapis.com, monitoring.googleapis.com, compute.googleapis.com, dns.googleapis.com, artifactregistry.googleapis.com, servicenetworking.googleapis.com |



### 1.3 Environments


Configured environments: **Development, Staging, Production, Sandbox**


---

## 2. Identity & Access Management

### 2.1 Administrative Groups


| Group Name | Purpose | Roles |
|------------|---------|-------|

| `gcp-organization-admins@acme.com` | org_admin | roles/resourcemanager.organizationAdmin |

| `gcp-billing-admins@acme.com` | billing_admin | roles/billing.admin |

| `gcp-network-admins@acme.com` | network_admin | roles/compute.networkAdmin, roles/compute.securityAdmin |

| `gcp-security-admins@acme.com` | security_admin | roles/iam.securityAdmin, roles/accesscontextmanager.policyAdmin |

| `gcp-audit-viewers@acme.com` | audit_viewer | roles/iam.securityReviewer, roles/logging.viewer |

| `gcp-support-admins@acme.com` | support_admin | roles/cloudsupport.techSupportEditor |





### 2.3 Service Accounts


| Name | Project | Purpose | Roles |
|------|---------|---------|-------|

| `terraform-org-sa` | prj-seed-terraform | terraform_org | roles/resourcemanager.organizationAdmin |

| `terraform-network-sa` | prj-seed-terraform | terraform_network | roles/compute.networkAdmin, roles/compute.securityAdmin, roles/dns.admin |

| `terraform-security-sa` | prj-seed-terraform | terraform | roles/resourcemanager.organizationAdmin |

| `cicd-deploy-sa` | prj-seed-cicd | cicd | roles/clouddeploy.operator, roles/cloudbuild.builds.editor, roles/artifactregistry.writer |

| `security-scanner-sa` | prj-seed-security | security_scanner | roles/iam.securityReviewer, roles/securitycenter.sourcesViewer |



---

## 3. Networking

### 3.1 Network Architecture

| Attribute | Value |
|-----------|-------|
| Architecture Type | Hub and Spoke |

### 3.2 VPC Networks


| VPC Name | Project | Routing Mode | Purpose |
|----------|---------|--------------|---------|

| `vpc-hub` | prj-network-hub | GLOBAL | hub |

| `vpc-prod` | prj-network-prod | GLOBAL | production |

| `vpc-dev` | prj-network-dev | GLOBAL | non_production |



### 3.3 Subnets


| Subnet | VPC | Region | CIDR | Private Google Access |
|--------|-----|--------|------|----------------------|

| `sb-hub-us-central1` | vpc-hub | us-central1 | `10.0.0.0/20` | Yes |

| `sb-prod-us-central1` | vpc-prod | us-central1 | `10.1.0.0/20` | Yes |

| `sb-dev-us-central1` | vpc-dev | us-central1 | `10.2.0.0/20` | Yes |

| `sb-hub-us-west2` | vpc-hub | us-west2 | `10.128.0.0/20` | Yes |

| `sb-prod-us-west2` | vpc-prod | us-west2 | `10.129.0.0/20` | Yes |

| `sb-dev-us-west2` | vpc-dev | us-west2 | `10.130.0.0/20` | Yes |



---



## 4. Hybrid Connectivity

| Attribute | Value |
|-----------|-------|
| Connectivity Type | Dedicated Interconnect |

| VPN Type | HA VPN |
| Routing | Dynamic |




### 4.1 On-Premises Networks

| Network Name | CIDR Ranges |
|-------------|-------------|

| on-prem-network | 192.20.0.0/20 |




### 4.2 Hybrid DNS

| Setting | Value |
|---------|-------|
| Inbound Forwarding | Enabled |



---



## 5. Security Configuration

### 5.1 Organization Policies


15 organization policies configured:

| Constraint | Enforcement | Scope |
|---|---|---|

| compute.skipDefaultNetworkCreation | enforce | organization |

| compute.requireOsLogin | enforce | organization |

| compute.requireShieldedVm | enforce | organization |

| compute.disableSerialPortAccess | enforce | organization |

| compute.vmExternalIpAccess | deny_all | organization |

| compute.disableNestedVirtualization | enforce | organization |

| storage.uniformBucketLevelAccess | enforce | organization |

| storage.publicAccessPrevention | enforce | organization |

| sql.restrictPublicIp | enforce | organization |

| sql.restrictAuthorizedNetworks | enforce | organization |

| iam.disableServiceAccountKeyCreation | enforce | organization |

| iam.disableServiceAccountKeyUpload | enforce | organization |

| gcp.detailedAuditLoggingMode | enforce | organization |

| gcp.resourceLocations | allow_list | organization |

| iam.allowedPolicyMemberDomains | allow_list | organization |



---

## 6. Logging & Monitoring

### 6.1 Log Retention

| Setting | Value |
|---------|-------|
| Default Retention Period | 2555 days |


### 6.2 Custom Retention Buckets

| Bucket Name | Retention (Days) | Locked |
|-------------|-----------------|--------|

| audit-logs | 730 | Yes |

| security-logs | 365 | Yes |




### 6.3 Centralized Logging

| Setting | Value |
|---------|-------|
| Logging Project | prj-seed-logging |

| Aggregated Sinks | 3 configured |



---



## 7. Backup & Disaster Recovery

| Attribute | Value |
|-----------|-------|
| DR Strategy | Backup Restore |
| Failover Automation | Enabled |

| Default RPO | 1h |
| Default RTO | 15m |


| Primary Region | us-central1 |
| DR Region | us-east1 |



### 7.1 Backup Policies

| Policy Name | Resource Type | Frequency | Retention (Days) | Cross-Region |
|-------------|--------------|-----------|-----------------|-------------|

| hourly-compute-snapshots | compute_disk | hourly | 7 | Yes |

| daily-compute-snapshots | compute_disk | daily | 90 | Yes |

| continuous-sql-backup | cloud_sql | continuous | 30 | Yes |

| daily-gcs-versioning | cloud_storage | continuous | 90 | Yes |

| daily-bigquery-snapshots | bigquery | daily | 30 | No |




### 7.2 Failover Testing

| Setting | Value |
|---------|-------|
| Testing Frequency | quarterly |
| Test Type | partial |


---



## 8. Cost Management

### 8.1 Budgets


| Budget Name | Amount | Scope |
|-------------|--------|-------|

| Organization Budget | USD 100000 | billing_account |



---

## What Was Generated

This wizard generated **FAST factory YAML data files** — structured configuration that plugs directly into Google Cloud's [FAST Fabric](https://github.com/GoogleCloudPlatform/cloud-foundation-fabric/tree/master/fast) landing zone framework.

| Attribute | Value |
|-----------|-------|
| Output Format | FAST Factory YAML |
| Framework | Cloud Foundation Fabric (FAST) |

| Stages Generated | 5 |



### FAST Stages Overview

| Stage | Directory | Description |
|-------|-----------|-------------|

| Organization Setup | `org-setup/` | Folders, IAM bindings, org policies, tags, billing |

| Networking | `networking/` | VPC networks, subnets, firewall rules, DNS, VPNs |

| Security | `security/` | KMS keyrings, security projects, SCC |

| Project Factory | `project-factory/` | Workload projects (GKE, data, apps, compute, ops) |

| VPC Service Controls | `vpcsc/` | Service perimeters, access levels, ingress/egress policies |



### How to Deploy

#### Prerequisites

- [Cloud Foundation Fabric](https://github.com/GoogleCloudPlatform/cloud-foundation-fabric) repository cloned
- GCP Organization with appropriate permissions
- Terraform >= 1.7 installed
- A service account or user with Organization Admin privileges

#### Deployment Steps

1. **Clone FAST Fabric** (if not already done):
   ```bash
   git clone https://github.com/GoogleCloudPlatform/cloud-foundation-fabric.git
   cd cloud-foundation-fabric/fast
   ```

2. **Place the generated data files** into the corresponding FAST stage directories:


   - Copy `org-setup/` contents into the FAST `org-setup/` stage data directory

   - Copy `networking/` contents into the FAST `networking/` stage data directory

   - Copy `security/` contents into the FAST `security/` stage data directory

   - Copy `project-factory/` contents into the FAST `project-factory/` stage data directory

   - Copy `vpcsc/` contents into the FAST `vpcsc/` stage data directory



3. **Deploy stages in order**:


   - **Stage 0**: Organization Setup (`org-setup/`)

   - **Stage 1**: Networking (`networking/`)

   - **Stage 2**: Security (`security/`)

   - **Stage 3**: Project Factory (`project-factory/`)

   - **Stage 4**: VPC Service Controls (`vpcsc/`)



4. **Review and apply** each stage with Terraform:
   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

### FAST Data File Format

The generated YAML files use FAST's factory data format with `$`-interpolation tokens that are resolved at `terraform plan` time:

- `$iam_principals:...` — References to IAM identities
- `$project_ids:...` — References to project IDs from the FAST registry
- `$folder_ids:...` — References to folder IDs

These tokens ensure that cross-stage dependencies are resolved automatically by FAST.

### Getting Help

- **FAST Documentation**: See [FAST README](https://github.com/GoogleCloudPlatform/cloud-foundation-fabric/blob/master/fast/README.md)
- **Stage-specific docs**: Each FAST stage directory contains its own README
- **Community**: [r/googlecloud](https://reddit.com/r/googlecloud), [Stack Overflow](https://stackoverflow.com/questions/tagged/google-cloud-platform)


---

## Important Disclaimers

1. **No Warranty**: These configurations are generated based on your inputs. Review thoroughly before any deployment.

2. **Security Review Required**: Have your security team review IAM bindings and org policies before deployment.

3. **Cost Implications**: Deploying this infrastructure will incur GCP charges. Review the Cost Management section.


4. **Not Standalone**: The YAML data files require FAST Fabric modules to deploy. They are not standalone Terraform.


5. **Your Responsibility**: Actual deployment, testing, and maintenance are your responsibility.

---

## Contacts

| Role | Email |
|------|-------|
| Primary Contact | cloudteam@acme.com |

| Secondary Contact | cloud-team@gmail.com |


---

*Generated by Cloud Foundation Design Studio v1.0.0*