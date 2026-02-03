# DevSecOps Tools – Important Points to Remember

## 🐧 Linux
- Everything in Linux is a file
- Common commands: `ls`, `cd`, `grep`, `awk`, `sed`, `find`, `tar`
- Process monitoring: `ps`, `top`, `htop`
- Disk & memory: `df`, `du`, `free`
- Networking: `curl`, `wget`, `ping`, `ss`
- Logs are stored in `/var/log`
- File permissions: `rwx` → user / group / others
- Service management using `systemctl`

---

## 🌱 Git
- Distributed Version Control System
- Common workflow: clone → branch → commit → push → PR
- `git fetch` ≠ `git pull`
- `merge` vs `rebase`
- `reset` vs `revert`
- `.gitignore` avoids committing unwanted files
- Small, meaningful commits are best

---

## 🐙 GitHub
- Code hosting and collaboration platform
- Pull Requests enable code reviews
- Branch protection rules secure main branches
- GitHub Actions for CI/CD
- Secrets stored securely using GitHub Secrets
- Webhooks enable integrations

---

## 🤖 Ansible
- Agentless configuration management tool
- Uses YAML playbooks
- Idempotent in nature
- Inventory can be static or dynamic
- Key components:
  - Playbooks
  - Inventory
  - Roles
  - Modules
- Used for configuration, not provisioning

---

## 🏗️ Terraform
- Infrastructure as Code (IaC) tool
- Declarative configuration language
- State file (`terraform.tfstate`) tracks resources
- Remote state using S3 + DynamoDB lock
- Lifecycle:
  - `init`
  - `plan`
  - `apply`
  - `destroy`
- Providers: AWS, Azure, GCP
- Modules help reuse infrastructure code

---

## 🧩 Jenkins
- CI/CD automation server
- Pipeline as Code using Jenkinsfile
- Declarative pipelines preferred
- Master/Agent architecture
- Secure credential management
- Integrates with security tools (SonarQube, Trivy, GitLeaks)

---

## 🐳 Docker
- Lightweight containerization platform
- Containers are faster than VMs
- Best practices:
  - Use minimal base images
  - Multi-stage builds
  - Avoid running containers as root
- Images are immutable
- Volumes used for persistent storage
- Container registries: DockerHub, ECR

---

## ☸️ Kubernetes
- Container orchestration platform
- Core components:
  - Pod
  - Deployment
  - Service
  - ConfigMap
  - Secret
- Desired state management
- Auto-scaling using HPA
- Service types: ClusterIP, NodePort, LoadBalancer
- Security via RBAC and Network Policies

---

## 🔐 HashiCorp Vault
- Secure secrets management tool
- Prevents hardcoding of secrets
- Supports dynamic secrets
- Authentication methods:
  - AppRole
  - Kubernetes
  - Cloud IAM
- Secret rotation supported
- Provides encryption and PKI services

---

## 📊 SonarQube
- Static code analysis tool
- Detects bugs, vulnerabilities, and code smells
- Quality Gates enforce code quality
- Integrates with CI/CD pipelines
- Supports multiple programming languages

---

## 🔎 GitLeaks
- Detects hardcoded secrets
- Scans Git repositories and history
- Prevents secret leaks in CI pipelines
- Can be used as pre-commit hook

---

## 🛡️ Trivy
- Vulnerability scanning tool
- Scans:
  - Docker images
  - File systems
  - Kubernetes clusters
  - IaC
- Detects CVEs, misconfigurations, and secrets
- Easy CI/CD integration

---

## 📦 Syft
- Generates Software Bill of Materials (SBOM)
- Scans container images and filesystems
- Identifies application dependencies
- Used for supply chain security

---

## 🧨 Grype
- Vulnerability scanner for SBOMs
- Works with Syft
- Identifies known CVEs
- Enhances supply chain security

---

## ✍️ Cosign
- Signs and verifies container images
- Prevents image tampering
- Supports keyless signing using OIDC
- Integrates with Kubernetes admission controllers
- Ensures image authenticity

---

## ⚡ GitHub Actions
- CI/CD platform integrated with GitHub
- Workflow files written in YAML
- Supports self-hosted and GitHub-hosted runners
- Secrets managed securely
- Triggered by events like push and pull requests

---

## 🔵 Azure DevOps
- End-to-end DevOps platform
- Includes:
  - Repos
  - Pipelines
  - Boards
  - Artifacts
- YAML and classic pipelines supported
- Strong integration with Azure

---

## ☁️ AWS
- Leading cloud service provider
- Core services:
  - EC2
  - S3
  - IAM
  - VPC
  - EKS
- IAM manages access and permissions
- Follows Shared Responsibility Model
- API-driven infrastructure

---

## ☁️ Azure
- Microsoft cloud platform
- Core services:
  - Virtual Machines
  - Blob Storage
  - Azure Active Directory
  - Virtual Network
  - AKS
- Enterprise-focused cloud
- RBAC is central to security

---

## ☁️ GCP
- Google Cloud Platform
- Core services:
  - Compute Engine
  - Cloud Storage
  - IAM
  - VPC
  - GKE
- Kubernetes-native platform
- Projects define resource boundaries

---

## 🎯 Interview Tip
Explain every tool using:
1. What it is  
2. Why it’s used  
3. Where you used it  
4. How it improves security or automation
