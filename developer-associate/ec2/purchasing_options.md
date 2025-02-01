# EC2 Instances Purchasing Options

## Overview of Purchasing Options
AWS offers multiple EC2 purchasing options to optimize costs based on workload requirements. Below is a breakdown of each option.

---

## 1. On-Demand Instances
- **Description**: Pay-as-you-go pricing with no upfront commitment.
- **Billing**: 
  - **Linux/Windows**: Per-second billing after the first minute.
  - **Other OS**: Per-hour billing.
- **Use Cases**: 
  - Short-term, unpredictable workloads.
  - Applications with flexible start/end times.
- **Key Features**:
  - Highest cost (no discounts).
  - No long-term commitments.
  - Recommended for testing or burstable workloads.

---

## 2. Reserved Instances (RIs)
- **Description**: Commit to 1- or 3-year terms for long-term workloads.
- **Discounts**: Up to **72% off** compared to On-Demand.
- **Types**:
  - **Standard RIs**: Fixed instance attributes (type, region, OS).
  - **Convertible RIs**: Flexible instance attributes (type, family, OS) with **66% discount**.
- **Payment Options**:
  - No Upfront | Partial Upfront | All Upfront (max discount).
- **Scope**:
  - **Regional**: Reserve capacity in a region.
  - **Zonal**: Reserve capacity in a specific AZ.
- **Use Cases**:
  - Steady-state workloads (e.g., databases).
  - Applications with predictable usage.
- **Marketplace**: Sell unused RIs in the Reserved Instance Marketplace.

---

## 3. Savings Plans
- **Description**: Commit to a **consistent usage amount** (measured in $/hour) for 1–3 years.
- **Discounts**: Up to **70% off** (same as RIs).
- **Flexibility**:
  - Locked to an instance family and region (e.g., `M5` in `us-east-1`).
  - Flexible across instance size, OS, and tenancy.
- **Use Cases**:
  - Long-term workloads with variable resource needs.
  - Cost optimization without instance-type rigidity.

---

## 4. Spot Instances
- **Description**: Bid on unused EC2 capacity for massive discounts.
- **Discounts**: Up to **90% off** compared to On-Demand.
- **Key Features**:
  - Instances can be terminated **immediately** if spot price > your bid.
  - No reliability guarantees.
- **Use Cases**:
  - Fault-tolerant workloads (e.g., batch processing, distributed jobs).
  - Flexible start/end times (e.g., image rendering, data analysis).
- **Avoid For**: Critical workloads (e.g., databases, production servers).

---

## 5. Dedicated Hosts
- **Description**: Reserve a **physical server** for EC2 instances.
- **Pricing**:
  - On-Demand (per-second) or Reserved (1/3-year terms).
  - Most expensive option.
- **Use Cases**:
  - Regulatory/compliance requirements.
  - Legacy software with per-core/per-socket licensing.
  - Full control over hardware (e.g., hypervisor access).

---

## 6. Dedicated Instances
- **Description**: Instances running on hardware **dedicated to your account**.
- **Key Features**:
  - No control over instance placement.
  - May share hardware with other instances in your account.
- **Use Cases**:
  - Isolation from other AWS customers (no shared hardware).

---

## 7. Capacity Reservations
- **Description**: Reserve capacity in a specific AZ for On-Demand instances.
- **Key Features**:
  - No discounts (billed at On-Demand rates).
  - No time commitment (cancel anytime).
  - Combine with RIs/Savings Plans for discounts.
- **Use Cases**:
  - Short-term, uninterrupted workloads in a specific AZ.

---

## Pricing Comparison (Example: `m4.large` in `us-east-1`)
| Option                  | Discount (vs. On-Demand) | Example Price (Hourly) |
|-------------------------|--------------------------|------------------------|
| On-Demand               | 0%                       | $0.10                  |
| Spot Instances          | Up to 90%                | ~$0.04                 |
| Reserved (1-Year All Upfront) | 72%               | ~$0.028                |
| Savings Plans           | 70%                      | ~$0.03                 |
| Dedicated Host          | On-Demand Pricing        | $0.10                  |
| Capacity Reservations   | On-Demand Pricing        | $0.10                  |

---

## Analogy: Resort Pricing Model
1. **On-Demand**: Pay full price to stay whenever you want.
2. **Reserved**: Book a room for 1–3 years upfront for discounts.
3. **Savings Plans**: Commit to spending $X/month for flexible room upgrades.
4. **Spot Instances**: Bid for empty rooms at huge discounts (risk eviction).
5. **Dedicated Host**: Rent the entire resort building (your own hardware).
6. **Capacity Reservations**: Reserve a room (pay full price even if unused).

---

## Summary: When to Use Which?
- **On-Demand**: Short-term, unpredictable workloads.
- **Reserved/Savings Plans**: Long-term, steady-state workloads.
- **Spot Instances**: Fault-tolerant, flexible workloads.
- **Dedicated Hosts**: Compliance/licensing requirements.
- **Capacity Reservations**: Guaranteed capacity in a specific AZ.