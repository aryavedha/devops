# 🌐 AWS VPC – Important Points to Remember

## 🔹 VPC Basics
- **VPC (Virtual Private Cloud)** is a logically isolated network in AWS
- CIDR range: **/16 to /28**
- Default VPC includes:
  - Public subnets
  - Internet Gateway
  - Route table
  - Security Group & NACL
- Custom VPC provides **full control** (recommended for production)

---

## 🔹 Subnets
- Subnets are **Availability Zone (AZ) specific**
- **Public Subnet**
  - Route table → Internet Gateway (IGW)
- **Private Subnet**
  - No direct internet access
  - Uses **NAT Gateway / NAT Instance**
- One subnet cannot span multiple AZs

---

## 🔹 Internet Gateway (IGW)
- Enables **internet connectivity** for public subnets
- Must be:
  - Attached to a VPC
  - Added to route table (`0.0.0.0/0 → IGW`)
- Required for:
  - Public EC2 instances
  - Internet-facing Load Balancers (ALB/NLB)

---

## 🔹 NAT Gateway / NAT Instance
- Enables **outbound internet access** for private subnet resources
- **NAT Gateway**
  - Managed by AWS
  - Requires Elastic IP
  - Deployed in public subnet
- **NAT Instance**
  - EC2-based
  - Requires manual scaling and patching
- ❗ NAT allows **outbound traffic only**, not inbound

---

## 🔹 Route Tables
- Control traffic routing inside VPC
- Each subnet must be associated with **one route table**
- Main route table exists by default
- Common routes:
  - `local` → VPC CIDR
  - `0.0.0.0/0 → IGW / NAT`

---

## 🔹 Security Groups (SG)
- **Stateful firewall**
- Applied at **instance level**
- Rules:
  - Allow rules only
  - Separate inbound and outbound rules
- If inbound traffic is allowed, response traffic is automatically allowed

---

## 🔹 Network ACL (NACL)
- **Stateless firewall**
- Applied at **subnet level**
- Rules:
  - Allow and deny rules supported
  - Evaluated in numerical order
- Both inbound and outbound traffic must be explicitly allowed

---

## 🔹 Elastic IP (EIP)
- Static public IPv4 address
- Used with:
  - NAT Gateway
  - EC2 instances
- Charged if **unused or not associated**

---

## 🔹 VPC Peering
- Connects two VPCs privately
- Supports:
  - Same account
  - Cross-account
  - Cross-region
- ❌ No transitive routing
- CIDR blocks must **not overlap**

---

## 🔹 VPC Endpoints
- Access AWS services **privately** without internet
- Types:
  - **Gateway Endpoint** → S3, DynamoDB
  - **Interface Endpoint** → ENI-based (most AWS services)
- Improves security and reduces NAT costs

---

## 🔹 DNS in VPC
- DNS resolution and hostnames must be enabled
- Required for:
  - Public DNS names
  - Route 53 Private Hosted Zones

---

## 🔹 VPC Flow Logs
- Capture network traffic metadata
- Can be enabled for:
  - VPC
  - Subnet
  - Network Interface (ENI)
- Logs can be sent to:
  - CloudWatch Logs
  - Amazon S3

---

## 🔹 High Availability Best Practices
- Use multiple Availability Zones
- Deploy NAT Gateway per AZ
- Use Load Balancers across AZs
- Avoid single points of failure

---

## 🔹 Common Interview One-Liners 💡
- Security Groups are **stateful**, NACLs are **stateless**
- Subnets are **AZ-specific**
- NAT Gateway is deployed in a **public subnet**
- IGW enables **inbound and outbound internet access**
- VPC Peering is **non-transitive**
