# Validation Warnings

**0 error(s), 4 warning(s)**

## Architecture Scorecard

_0 error(s), 1 warning(s)_

### Security Baseline (06_security_baseline)

#### ⚠️ Security: CMEK enabled but no key rings configured. The CMEK composer will auto-generate keys from workload services.
**Source:** Architecture Scorecard
**Impact:** Architecture scorecard deducted 5 points
**How to fix:** Review the Security Baseline section and address the finding

---

## Auto-Resolved References

_0 error(s), 3 warning(s)_

### GKE & Containers (12_gke_containers)

#### ⚠️ GKE VPC 'vpc-main' not found in networking; auto-resolved to 'vpc-prod'
**Source:** Auto-Resolved References
**Field:** `networking_config.vpc_network`
**Impact:** Auto-resolved: networking_config.vpc_network changed from 'vpc-main' to 'vpc-prod'
**How to fix:** Verify the auto-resolved value in GKE & Containers
**Recommended value:** `vpc-prod`

#### ⚠️ GKE subnet 'sb-main-{{primary_region}}' not found; auto-resolved to 'sb-prod-us-central1'
**Source:** Auto-Resolved References
**Field:** `networking_config.subnet`
**Impact:** Auto-resolved: networking_config.subnet changed from 'sb-main-{{primary_region}}' to 'sb-prod-us-central1'
**How to fix:** Verify the auto-resolved value in GKE & Containers
**Recommended value:** `sb-prod-us-central1`

### Hybrid Connectivity (05_hybrid_connectivity)

#### ⚠️ VLAN attachment 'vlan-attach-prod' references router 'router-prod' which didn't exist; auto-generated router in us-central1 on vpc-prod
**Source:** Auto-Resolved References
**Field:** `cloud_routers.router-prod`
**Impact:** Auto-resolved: cloud_routers.router-prod changed from '(missing)' to 'router-prod'
**How to fix:** Verify the auto-resolved value in Hybrid Connectivity
**Recommended value:** `router-prod`

---
