# 🎯 DevSecOps Interview Golden Rule

For **every tool**, explain:
1. What it is  
2. Why it’s used  
3. Where you used it  
4. How it improves **security, automation, or reliability**

---

# DevSecOps Tools – Important Points to Remember (Deep Dive)

---

## 🐧 Linux

### Key Concepts
- Everything in Linux is a file (configs, devices, sockets)
- Base OS for servers, containers, and CI/CD agents
- Process-based architecture
- Environment variables are critical in CI/CD
- Cron jobs automate recurring tasks

### System & Operations
- Logs stored in `/var/log` (important for RCA)
- Systemd for service management
- Permissions and ownership control access
- Linux security features:
  - SUID, SGID, Sticky bit
  - ACLs (`setfacl`)

### Common Commands
- File operations: `ls`, `cp`, `mv`, `rm`, `stat`
- Text processing: `grep`, `awk`, `sed`, `cut`, `sort`, `uniq`
- Process management: `ps`, `top`, `htop`, `nice`, `kill`
- Disk & memory: `df`, `du`, `free`, `lsblk`, `mount`
- Networking: `ss`, `netstat`, `tcpdump`, `iptables`
- Logs: `journalctl`, `/var/log/syslog`

---

## 🌱 Git

### Key Concepts
- Distributed Version Control System (DVCS)
- Every developer has a full repository copy
- Git uses **SHA-1 hashing** for data integrity
- Lightweight and fast branching
- Backbone of CI/CD and GitOps

### Core Workflow
- Clone → Branch → Commit → Push → Pull Request
- `git fetch` downloads changes only
- `git pull` = fetch + merge
- `merge` preserves history
- `rebase` rewrites history

### Advanced Usage
- `git stash` saves uncommitted changes
- `git cherry-pick` applies specific commits
- Tags for releases (lightweight vs annotated)
- Git hooks enable automation
- History is immutable unless rewritten

---

## 🐙 GitHub

### Key Concepts
- Cloud-based Git repository hosting
- Acts as a DevOps collaboration platform
- Often the single source of truth

### Security & Collaboration
- Pull Requests enforce review policies
- CODEOWNERS control approvals
- Branch protection rules prevent risky merges
- GitHub Secrets encrypt sensitive values
- Dependabot detects vulnerable dependencies
- GitHub Advanced Security supports:
  - SAST
  - Secret scanning

### Automation
- GitHub Actions provides CI/CD
- Environments support approval gates
- Webhooks integrate external tools (Jenkins, Slack)
- Marketplace offers reusable actions

---

## 🤖 Ansible

### Key Concepts
- Agentless configuration management
- Push-based model using SSH
- Playbooks written in YAML
- Idempotent execution

### Architecture
- Inventory defines managed hosts
- Roles improve reuse and structure
- Variables and Jinja2 templates enable dynamic configs
- Facts collect system information

### Security & Operations
- Ansible Vault encrypts secrets
- Dry run support (`--check`)
- Used for:
  - Patch management
  - Middleware configuration
  - Server hardening

---

## 🏗️ Terraform

### Key Concepts
- Infrastructure as Code (IaC)
- Declarative syntax using HCL
- Manages infrastructure lifecycle

### State & Team Usage
- State file tracks resources and is sensitive
- Remote state prevents team conflicts
- State locking avoids concurrent changes
- Drift detection identifies manual changes

### Advanced Features
- Modules promote DRY principles
- Workspaces manage environments
- Dependency graph controls execution order
- Terraform Cloud supports policy enforcement
- Not intended for in-server configuration

---

## 🧩 Jenkins

### Key Concepts
- Open-source CI/CD automation server
- Pipeline as Code using Jenkinsfile
- Declarative pipelines preferred

### Pipeline Capabilities
- Parallel and sequential stages
- Shared libraries for reuse
- Manual approval gates
- Blue Ocean UI

### Security & Ops
- Credentials stored securely
- Integrates SAST, DAST, container scans
- Commonly runs on Kubernetes
- Requires plugin and security maintenance

---

## 🐳 Docker

### Key Concepts
- Containerization platform
- Packages application with dependencies
- Faster startup than VMs
- Uses Linux kernel features:
  - Namespaces
  - Cgroups

### Best Practices
- Minimal base images
- Multi-stage builds
- Avoid running as root
- Containers should be stateless
- Images are immutable and versioned

### Security
- `.dockerignore` reduces attack surface
- Read-only filesystems
- Image scanning before deployment

---

## ☸️ Kubernetes

### Key Concepts
- Container orchestration platform
- Control plane + worker node architecture
- Pod is the smallest deployable unit

### Core Objects
- Pod
- Deployment
- ReplicaSet
- Service
- ConfigMap
- Secret

### Reliability & Scaling
- Desired state reconciliation
- Self-healing workloads
- HPA for auto-scaling
- Rolling updates and rollbacks

### Security
- RBAC
- Namespaces
- Network Policies
- Pod Security Standards
- Admission Controllers

---

## 🔐 HashiCorp Vault

### Key Concepts
- Centralized secrets management
- Encrypts secrets at rest and in transit
- Eliminates hardcoded credentials

### Security Features
- Dynamic, short-lived secrets
- Token-based access
- Policies control permissions
- Audit logs track secret access
- Kubernetes auto-injection support

### Architecture
- Fits Zero Trust model
- Supports AppRole, Kubernetes, cloud IAM

---

## 📊 SonarQube

### Key Concepts
- Static Application Security Testing (SAST)
- Enforces code quality standards

### Capabilities
- Detects bugs, vulnerabilities, code smells
- Measures code coverage and technical debt
- Quality Gates block insecure code
- Integrates with PR checks
- Supports shift-left security

---

## 🔎 GitLeaks

### Key Concepts
- Secret detection tool
- Regex-based scanning
- Lightweight and fast

### Usage
- Scans commits, branches, and history
- Detects API keys, passwords, tokens
- Used as:
  - Pre-commit hook
  - CI pipeline step
- Important for SOC2 / ISO compliance

---

## 🛡️ Trivy

### Key Concepts
- Vulnerability and misconfiguration scanner
- Popular open-source DevSecOps tool

### Capabilities
- Scans:
  - Container images
  - Filesystems
  - Kubernetes clusters
  - IaC (Terraform, Helm)
- Detects CVEs and exposed secrets
- Severity-based pipeline failures
- Uses multiple vulnerability databases

---

## 📦 Syft

### Key Concepts
- Generates Software Bill of Materials (SBOM)
- Improves supply-chain visibility

### Capabilities
- Lists all dependencies
- Supports SPDX and CycloneDX formats
- Works offline
- Required for audits and compliance
- Used before vulnerability scanning

---

## 🧨 Grype

### Key Concepts
- Vulnerability scanner for SBOMs
- Works with Syft output

### Capabilities
- Maps dependencies to known CVEs
- Provides severity ratings
- Supports policy enforcement
- Strengthens supply-chain security

---

## ✍️ Cosign

### Key Concepts
- Container image signing and verification
- Part of the Sigstore project

### Security
- Ensures image authenticity and integrity
- Prevents tampering
- Supports keyless signing via OIDC
- Uses transparency logs
- Integrates with CI/CD and Kubernetes admission controllers

---

## ⚡ GitHub Actions

### Key Concepts
- GitHub-native CI/CD platform
- Workflow defined in YAML

### Capabilities
- Event-driven pipelines
- Matrix builds
- Reusable workflows
- Environment-based approvals
- Secrets masking
- OIDC support for cloud authentication
- Ideal for GitOps workflows

---

## 🔵 Azure DevOps

### Key Concepts
- Enterprise DevOps platform from Microsoft

### Components
- Repos
- Pipelines
- Boards
- Artifacts

### Capabilities
- YAML and classic pipelines
- Linux and Windows agents
- Agile & Scrum planning
- Strong Azure and Kubernetes integration
- Role-based access control

---

## ☁️ AWS

### Key Concepts
- Largest cloud service provider
- API-driven infrastructure

### Core Services
- EC2, S3, IAM, VPC, EKS

### Security & Operations
- IAM roles preferred over users
- Least privilege principle
- Shared Responsibility Model
- Security services:
  - GuardDuty
  - Inspector
  - Security Hub
- Logging with CloudTrail and CloudWatch

---

## ☁️ Azure

### Key Concepts
- Microsoft cloud platform
- Strong enterprise and hybrid support

### Core Services
- VM
- Blob Storage
- Azure AD
- VNet
- AKS

### Security
- Azure AD is identity backbone
- RBAC and Azure Policy enforce compliance
- Defender for Cloud improves posture
- Tight Microsoft ecosystem integration

---

## ☁️ GCP

### Key Concepts
- Kubernetes-first cloud platform

### Core Services
- Compute Engine
- Cloud Storage
- IAM
- VPC
- GKE

### Strengths
- Fine-grained IAM
- Strong default security
- High-performance networking
- Preferred for data and ML workloads

---

## 🏆 DevSecOps Master Rule

DevSecOps is about:
- **Automation**
- **Security by default**
- **Shift-left testing**
- **Continuous monitoring**
- **Infrastructure as Code**
