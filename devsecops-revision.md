# DevSecOps Tools – Important Points to Remember (Deep Dive)

## 🐧 Linux
- Everything is a file (including devices and sockets)
- Linux follows **process-based architecture**
- Common commands:
  - File ops: `ls`, `cp`, `mv`, `rm`, `stat`
  - Text processing: `grep`, `awk`, `sed`, `cut`, `sort`, `uniq`
- Process management:
  - `ps`, `top`, `htop`, `nice`, `kill`, `killall`
- Disk & memory:
  - `df`, `du`, `free`, `lsblk`, `mount`
- Networking:
  - `ss`, `netstat`, `tcpdump`, `iptables`
- Logs:
  - `/var/log/messages`, `/var/log/syslog`
  - `journalctl` for systemd logs
- Permissions & security:
  - `chmod`, `chown`, `setfacl`
  - SUID, SGID, Sticky bit
- Cron & system automation:
  - `crontab`, `at`
- Linux is the base OS for most DevOps tools

---

## 🌱 Git
- Git uses **SHA-1 hashing** for integrity
- Branching is lightweight and fast
- Staging area allows selective commits
- `git cherry-pick` applies specific commits
- `git stash` temporarily saves work
- Tags:
  - Lightweight vs annotated
- Git hooks enable automation (pre-commit, pre-push)
- Git history is immutable (unless rewritten)
- Git enables **GitOps workflows**

---

## 🐙 GitHub
- GitHub is a **DevOps collaboration platform**
- Pull Requests enforce code quality
- CODEOWNERS enforce review policies
- GitHub Actions marketplace provides reusable actions
- Environments support approval gates
- Dependabot checks dependency vulnerabilities
- GitHub Advanced Security supports SAST & secret scanning
- GitHub integrates well with GitOps tools

---

## 🤖 Ansible
- Push-based configuration management
- Uses Python-based modules
- Facts gather system information
- `ansible-playbook --check` for dry runs
- Handlers run only when notified
- Ansible Galaxy provides reusable roles
- Vault encrypts secrets inside playbooks
- Used for:
  - Patch management
  - Middleware configuration
  - Server hardening

---

## 🏗️ Terraform
- Terraform manages **infrastructure lifecycle**
- Uses dependency graph for execution order
- State file stores sensitive data → must be secured
- Supports:
  - `count`
  - `for_each`
  - `depends_on`
- Workspaces manage multiple environments
- Drift detection identifies manual changes
- Terraform Cloud provides policy enforcement
- Common in GitOps + IaC pipelines

---

## 🧩 Jenkins
- Jenkins supports:
  - Freestyle jobs
  - Declarative pipelines
- Pipelines are version-controlled
- Shared libraries promote reuse
- Blue Ocean provides better UI
- Supports manual approval gates
- Can integrate DAST/SAST tools
- Jenkins often runs in Kubernetes
- Requires maintenance and security hardening

---

## 🐳 Docker
- Docker uses Linux kernel features:
  - Namespaces
  - Cgroups
- Image layers improve caching
- `docker inspect` helps debugging
- `.dockerignore` reduces image size
- Containers should be stateless
- Docker security:
  - Read-only filesystems
  - Non-root users
- Docker is often combined with Kubernetes

---

## ☸️ Kubernetes
- Kubernetes follows **control plane + worker node model**
- Control plane components:
  - API Server
  - Scheduler
  - Controller Manager
- Pod is the smallest deployable unit
- Health checks:
  - Liveness
  - Readiness
- ConfigMaps & Secrets externalize config
- Rolling updates ensure zero downtime
- Security:
  - Pod Security Standards
  - Admission Controllers
- Kubernetes is core to cloud-native DevSecOps

---

## 🔐 HashiCorp Vault
- Vault encrypts secrets at rest and in transit
- Uses tokens for access
- Supports namespaces (enterprise)
- Dynamic secrets reduce blast radius
- Integrated with Kubernetes for auto-injection
- Audit logs track secret access
- Vault fits Zero Trust security model

---

## 📊 SonarQube
- Performs **Static Application Security Testing (SAST)**
- Enforces coding standards
- Measures:
  - Code coverage
  - Technical debt
- Integrates with PR checks
- Quality Profiles customize rules
- Used early in SDLC (shift-left)

---

## 🔎 GitLeaks
- Regex-based secret detection
- Supports custom rules
- Can block commits automatically
- Scans both local and remote repos
- Important for compliance (SOC2, ISO)
- Lightweight and fast

---

## 🛡️ Trivy
- Uses multiple vulnerability databases
- Scans OS and application dependencies
- Supports severity-based pipeline failures
- Can scan running Kubernetes clusters
- Detects misconfigured resources
- Essential DevSecOps security scanner

---

## 📦 Syft
- Generates SBOM in multiple formats
- Supports SPDX & CycloneDX
- Helps with compliance (SBOM mandates)
- Works offline
- Improves dependency transparency

---

## 🧨 Grype
- Consumes SBOM from Syft
- Identifies vulnerabilities across dependencies
- Provides severity ratings
- Supports policy enforcement
- Strengthens supply chain security

---

## ✍️ Cosign
- Part of Sigstore project
- Signs images using cryptographic signatures
- Supports transparency logs
- Enables trusted deployments
- Prevents malicious image usage
- Integrates with CI/CD pipelines

---

## ⚡ GitHub Actions
- Supports reusable workflows
- Matrix builds for multi-env testing
- Environment-based approvals
- Secrets are masked in logs
- Supports OIDC for cloud auth
- Ideal for GitOps pipelines

---

## 🔵 Azure DevOps
- Supports enterprise-scale DevOps
- Azure Pipelines supports Linux & Windows agents
- Artifacts manage packages
- Boards support Agile & Scrum
- Integrates with Terraform & Kubernetes
- Strong role-based access control

---

## ☁️ AWS
- IAM roles preferred over users
- Security services:
  - GuardDuty
  - Inspector
  - Security Hub
- Logging:
  - CloudTrail
  - CloudWatch
- Highly available & scalable
- Backbone of many DevSecOps setups

---

## ☁️ Azure
- Azure AD centralizes identity
- Strong hybrid cloud support
- Azure Policy enforces compliance
- Defender for Cloud improves security posture
- Tight integration with Microsoft tools

---

## ☁️ GCP
- IAM uses fine-grained permissions
- Strong Kubernetes (GKE)
- Built-in security defaults
- Excellent networking performance
- Preferred for data-heavy workloads

---

## 🏆 DevSecOps Master Rule
DevSecOps is about:
- **Automation**
- **Security by default**
- **Shift-left testing**
- **Continuous monitoring**
- **Infrastructure as Code**
