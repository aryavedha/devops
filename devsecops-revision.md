# 🎯 DevSecOps Interview Golden Rule

For **every tool**, be ready to explain:
1. **What it is**
2. **Why it’s used**
3. **Where you used it**
4. **How it improves security, automation, or reliability**

---

# 🚀 DevSecOps Tools – Important Points & Real-World Commands

---

## 🐧 Linux

### Key Concepts
- Everything in Linux is a file (configs, devices, sockets, logs)
- Base OS for servers, containers, and CI/CD agents
- Process-based architecture
- Environment variables are critical in CI/CD
- Cron jobs automate recurring tasks
- Logs are essential for RCA and monitoring

### Security & Operations
- Logs stored in `/var/log`
- `systemd` for service management
- File permissions and ownership control access
- Linux security features:
  - SUID, SGID, Sticky Bit
  - ACLs (`setfacl`)

### Real-World Commands
```bash
ps aux
top
htop
uptime

df -h
du -sh *
free -m
lsblk

tail -f /var/log/syslog
journalctl -u docker
journalctl -xe

ss -tulnp
curl -I https://example.com
ping google.com

chmod 755 file.sh
chown user:group file

```
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

```
git clone <repo_url>
git status
git branch
git checkout -b feature-branch
git add .
git commit -m "message"
git push origin feature-branch

git fetch
git pull
git rebase main
git cherry-pick <commit_id>
git revert <commit_id>
git stash
```

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

```
ansible --version
ansible all -i inventory -m ping
ansible-playbook playbook.yml
ansible-playbook playbook.yml --check
ansible-playbook playbook.yml --tags nginx

ansible-vault encrypt secrets.yml
ansible-vault decrypt secrets.yml

```
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

```
terraform init
terraform validate
terraform plan
terraform apply
terraform destroy

terraform state list
terraform state show <resource>
terraform workspace list
terraform workspace select dev

```
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

```
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
  }
}

```
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

```
docker version
docker build -t myapp:1.0 .
docker images
docker run -d -p 80:80 myapp
docker ps
docker logs <container_id>
docker exec -it <container_id> sh
docker stop <container_id>
docker rm <container_id>

```
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

```
kubectl get nodes
kubectl get pods
kubectl get svc
kubectl describe pod <pod_name>
kubectl logs <pod_name>
kubectl exec -it <pod_name> -- sh

kubectl apply -f deployment.yml
kubectl delete -f deployment.yml
kubectl rollout status deployment <app>
kubectl scale deployment <app> --replicas=3

```
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

```
vault status
vault login
vault secrets list
vault kv get secret/db
vault kv put secret/db password=123
vault auth list
vault policy list

```
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

```
sonar-scanner \
  -Dsonar.projectKey=myapp \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://sonarqube:9000 \
  -Dsonar.login=$SONAR_TOKEN

```
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

```
gitleaks detect
gitleaks detect --source .
gitleaks detect --redact
gitleaks protect --staged

```
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

```
trivy image nginx:latest
trivy image --severity HIGH,CRITICAL myapp:1.0
trivy fs .
trivy config .
trivy k8s cluster

```

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

```
syft myapp:1.0
syft myapp:1.0 -o json
syft dir:.

```

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

```
grype myapp:1.0
grype sbom:sbom.json
grype myapp:1.0 --severity critical

```
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

```
cosign generate-key-pair
cosign sign --key cosign.key myapp:1.0
cosign verify --key cosign.pub myapp:1.0

```
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

```
name: CI Pipeline
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: docker build -t myapp .
```
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

```
trigger:
- main

steps:
- script: terraform plan
- script: terraform apply -auto-approve

```
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

```
aws configure
aws ec2 describe-instances
aws s3 ls
aws s3 cp file.txt s3://bucket
aws eks update-kubeconfig --name cluster

```
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

```
az login
az account list
az vm list
az aks get-credentials --name cluster --resource-group rg

```
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

```
gcloud auth login
gcloud config list
gcloud compute instances list
gcloud container clusters get-credentials cluster

```
---

## 🏆 DevSecOps Master Rule

DevSecOps is about:
- **Automation**
- **Security by default**
- **Shift-left testing**
- **Continuous monitoring**
- **Infrastructure as Code**
