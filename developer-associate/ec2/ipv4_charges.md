# IPv4 Charges in AWS (Effective Feb 1, 2024)

## Overview
AWS now charges **$0.005 per hour** ($3.6/month) for **every Public IPv4 address** in your account, whether used or unused. This applies across all services except for limited EC2 free-tier allowances.

---

## Key Details
### 1. **EC2 Free Tier (New Accounts)**
- **750 hours/month** of Public IPv4 usage for the first **12 months**.
- **Example**:
  - Running **1 EC2 instance** with a Public IPv4 for a full month (750 hours) → **$0**.
  - Running **2 EC2 instances** with Public IPv4s for 750 hours each → **$3.6/month** (billed for the extra 750 hours).

### 2. **Non-EC2 Services**
- **No free tier** for Public IPv4 addresses.
- **Examples**:
  - **Load Balancer**: 1 Public IPv4 per AZ. A 3-AZ load balancer → 3 Public IPv4s → **$10.8/month**.
  - **Amazon RDS**: Public IPv4 charges apply if the database is publicly accessible.

### 3. **IPv6 Considerations**
- IPv6 addresses are **free** (AWS encourages migration to IPv6).
- **Why IPv6 isn’t used in this course**:
  - Some ISPs/regions lack IPv6 support (test at [test-ipv6.com](https://test-ipv6.com/)).
  - Complexity for beginners (requires custom security groups/networking rules).

---

## Troubleshooting Charges
### 1. **AWS Billing Dashboard**
- **Steps**:
  1. Go to **Billing & Cost Management** → **Bills**.
  2. Under **Bill Details**, expand **Service Charges**.
  3. Look for **EC2** or **Other Services** with line items for `PublicIPv4` or `Public IP`.

### 2. **Amazon VPC IP Address Manager (IPAM)**
- **Steps**:
  1. Search for **IPAM** in the AWS Console.
  2. Create an **IPAM** (free tier eligible) → Enable **Public IP Insights**.
  3. Select regions to monitor → Analyze Public IPv4 usage across services.

### 3. **AWS Public IP Insights**
- **Use Case**: Identify unused/lingering Public IPv4 addresses.
- **Documentation**: [AWS Troubleshooting Guide](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/troubleshooting-public-ip-charges.html).

---

## Cost-Saving Tips
1. **Terminate Unused Resources**:
   - Delete EC2 instances, load balancers, or RDS databases when not in use.
2. **Use Elastic IPs Sparingly**:
   - Elastic IPs incur charges if not attached to a running instance.
3. **Migrate to IPv6** (Advanced):
   - Configure IPv6 for eligible workloads (requires networking expertise).

---

## Example Charges Breakdown
| Service               | Public IPv4s | Monthly Cost (Per IP) | Total Cost (Example)        |
|-----------------------|--------------|-----------------------|------------------------------|
| EC2 (Free Tier)       | 1            | $0 (750 hours)        | $0                            |
| EC2 (Post-Free Tier)  | 2            | $3.6 each             | $7.2                         |
| Load Balancer (3 AZs) | 3            | $3.6 each             | $10.8                        |
| RDS Database          | 1            | $3.6                  | $3.6                         |

---

> **Warning**: Always clean up resources after labs/hands-on to avoid unexpected charges!