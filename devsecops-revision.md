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

    environment {
        APP_NAME = "demo-app"
        DOCKER_IMAGE = "aryavedha/demo-app"
        DOCKER_TAG = "${BUILD_NUMBER}"
    }

    tools {
        maven 'maven-3.9'
        jdk 'jdk-17'
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning source code..."
                git branch: 'main',
                    url: 'https://github.com/your-org/demo-app.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building application..."
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Unit Tests') {
            steps {
                echo "Running unit tests..."
                sh 'mvn test'
            }
        }

        stage('Code Quality Scan (SonarQube)') {
            steps {
                echo "Running SonarQube scan..."
                withSonarQubeEnv('sonarqube-server') {
                    sh '''
                      mvn sonar:sonar \
                      -Dsonar.projectKey=demo-app \
                      -Dsonar.projectName=demo-app
                    '''
                }
            }
        }

        stage('Security Scan (Trivy)') {
            steps {
                echo "Scanning filesystem for vulnerabilities..."
                sh 'trivy fs --exit-code 0 --severity HIGH,CRITICAL .'
            }
        }

        stage('Docker Build') {
            steps {
                echo "Building Docker image..."
                sh """
                  docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .
                """
            }
        }

        stage('Docker Push') {
            steps {
                echo "Pushing image to Docker Hub..."
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                      echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                      docker push ${DOCKER_IMAGE}:${DOCKER_TAG}
                    """
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                echo "Deploying to Kubernetes..."
                sh '''
                  kubectl set image deployment/demo-app \
                  demo-app=${DOCKER_IMAGE}:${DOCKER_TAG} -n demo
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Check logs."
        }
        always {
            cleanWs()
        }
    }
}

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
k8s demo manifest file
1️⃣ Namespace
```
apiVersion: v1
kind: Namespace
metadata:
  name: demo-app
```
2️⃣ ConfigMap (app configuration)
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-config
  namespace: demo-app
data:
  index.html: |
    <html>
      <body style="font-family: Arial">
        <h1>Welcome to Demo App 🚀</h1>
        <p>Running on Kubernetes</p>
      </body>
    </html>
```
3️⃣ Secret (simulating sensitive data)
```
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
  namespace: demo-app
type: Opaque
data:
  DB_PASSWORD: cGFzc3dvcmQxMjM=   # password123 (base64)
```

4️⃣ Deployment (real-world settings)
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: demo-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.25
        ports:
        - containerPort: 80
        env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: app-secret
              key: DB_PASSWORD
        volumeMounts:
        - name: web-content
          mountPath: /usr/share/nginx/html
        resources:
          requests:
            cpu: "100m"
            memory: "128Mi"
          limits:
            cpu: "300m"
            memory: "256Mi"
      volumes:
      - name: web-content
        configMap:
          name: nginx-config
```

5️⃣ Service (internal exposure)
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: demo-app
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
```

6️⃣ Ingress (real-world access)
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress
  namespace: demo-app
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  rules:
  - host: demo.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginx-service
            port:
              number: 80
```
7️⃣ HPA (Auto-Scaling)
```
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: nginx-hpa
  namespace: demo-app
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-deployment
  minReplicas: 2
  maxReplicas: 5
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 60

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
Ansible playdook demo
```
---
- name: Demo Ansible Playbook – Setup Nginx Web Server
  hosts: webservers
  become: yes
  vars:
    app_name: demo-app
    index_content: |
      <html>
        <body style="font-family: Arial; text-align: center;">
          <h1>Welcome to {{ app_name }} 🚀</h1>
          <p>Deployed via Ansible!</p>
        </body>
      </html>

  tasks:

    - name: Update APT package cache
      ansible.builtin.apt:
        update_cache: yes

    - name: Install Nginx
      ansible.builtin.apt:
        name: nginx
        state: present

    - name: Ensure Nginx is started and enabled
      ansible.builtin.service:
        name: nginx
        state: started
        enabled: yes

    - name: Deploy index.html page
      ansible.builtin.copy:
        content: "{{ index_content }}"
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'

    - name: Open HTTP port in UFW firewall (if enabled)
      ansible.builtin.ufw:
        rule: allow
        name: 'Nginx Full'
      ignore_errors: yes

    - name: Verify Nginx is running
      ansible.builtin.shell: curl -s http://localhost
      register: curl_result

    - name: Show deployed page content
      ansible.builtin.debug:
        msg: "{{ curl_result.stdout }}"

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
# 🚀 DevSecOps Tools – Monitoring, Build, Runtime & Databases

---

## 🐚 Shell Scripting

### Key Concepts
- Automates repetitive Linux tasks
- Used heavily in CI/CD pipelines
- Glue between tools (Git, Docker, Cloud, Kubernetes)
- Bash is the most commonly used shell
- Scripts should be idempotent and error-aware

### Best Practices
- Use `#!/bin/bash`
- Enable strict mode:
  ```bash
  set -euo pipefail
Log outputs

Validate inputs

Avoid hardcoding secrets

Real-World Commands
```
#!/bin/bash

echo "Build started"
DATE=$(date)
echo "Date: $DATE"

if systemctl is-active docker; then
  echo "Docker is running"
else
  systemctl start docker
fi

for i in {1..5}; do
  echo "Iteration $i"
done

df -h | grep -v tmpfs
```
---
📈 Prometheus
Key Concepts
Time-series monitoring system

Pull-based metrics collection

Uses PromQL for querying

Stores metrics, not logs

Kubernetes-native monitoring tool

Architecture
Prometheus Server

Exporters (Node, App, Custom)

Alertmanager

Targets discovered via service discovery

Real-World Commands
```
# Check Prometheus targets
curl http://localhost:9090/targets

# Example PromQL
up
node_cpu_seconds_total
rate(http_requests_total[5m])
```
---
📊 Grafana
Key Concepts
Visualization and dashboarding tool

Works with Prometheus, Loki, CloudWatch, Elasticsearch

Used for monitoring and alerting

Role-based access control

Real-World Usage
Create dashboards for:

CPU / Memory

Pod health

API latency

Set alerts for SLA breaches

Real-World Commands
```
# Run Grafana
docker run -d -p 3000:3000 grafana/grafana

# Default login
admin / admin
```
---
📚 ELK Stack (Elasticsearch, Logstash, Kibana)
Key Concepts
Centralized logging solution

Elasticsearch stores and indexes logs

Logstash processes logs

Kibana visualizes logs

Use Cases
Application log analysis

Security auditing

Incident RCA

Observability

Real-World Commands
```
# Check Elasticsearch health
curl http://localhost:9200/_cluster/health

# List indices
curl http://localhost:9200/_cat/indices

# Common log path
/var/log/*.log
```
---
☁️ CloudWatch (AWS)
Key Concepts
Native AWS monitoring service

Collects logs, metrics, and events

Integrated with AWS services

Supports alarms and dashboards

Real-World Usage
Monitor EC2, EKS, Lambda

Centralized logging

Alerting on CPU, memory, errors

Real-World Commands
```
aws cloudwatch list-metrics
aws logs describe-log-groups
aws logs tail /aws/ec2/system --follow
```
---
🚨 Nagios
Key Concepts
Traditional infrastructure monitoring

Host and service monitoring

Plugin-based architecture

Alerting via email/SMS

Use Cases
Server availability

Disk, CPU, memory checks

Legacy environments

Real-World Commands
```
systemctl status nagios
/usr/local/nagios/libexec/check_disk -w 20% -c 10%
```
---
📦 Nexus Repository
Key Concepts
Artifact repository manager

Stores binaries and dependencies

Supports Maven, Docker, NPM, NuGet, PyPI

Prevents dependency loss

Use Cases
Dependency caching

Artifact versioning

Secure artifact distribution

Real-World Usage
```
# Docker login
docker login nexus.company.com

# Push image
docker push nexus.company.com/myapp:1.0
```
---
⎈ Helm
Key Concepts
Kubernetes package manager

Uses charts (templated YAML)

Manages application lifecycle

Simplifies Kubernetes deployments

Real-World Commands
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm search repo nginx
helm install myapp bitnami/nginx
helm list
helm upgrade myapp bitnami/nginx
helm uninstall myapp
```
---
🚀 Argo CD
Key Concepts
GitOps continuous delivery tool

Kubernetes-native

Git is the single source of truth

Automatic drift detection

Real-World Commands
```
argocd login localhost:8080
argocd app list
argocd app sync myapp
argocd app status myapp
```
---
🕸️ Service Mesh – Istio
Key Concepts
Manages service-to-service communication

Provides traffic management, security, observability

Uses Envoy sidecar proxies

Capabilities
mTLS

Traffic splitting

Circuit breaking

Retries and timeouts

Real-World Commands
```
istioctl install
kubectl get pods -n istio-system
istioctl analyze
```
---
🌐 Nginx
Key Concepts
Web server and reverse proxy

Load balancer

Common ingress controller in Kubernetes

Real-World Commands
```
nginx -t
systemctl restart nginx
tail -f /var/log/nginx/access.log
```
---
🌐 Apache HTTP Server
Key Concepts
Traditional web server

Module-based architecture

Common in legacy apps

Real-World Commands
```
apachectl configtest
systemctl restart httpd
tail -f /var/log/httpd/error_log
```
---
☕ Apache Tomcat
Key Concepts
Java application server

Runs WAR files

Used for Spring / Java apps

Real-World Commands
```
systemctl status tomcat
tail -f /opt/tomcat/logs/catalina.out
```
---
🛠️ Maven
Key Concepts
Java build and dependency management tool

Uses pom.xml

Standard lifecycle phases

Real-World Commands
```
mvn clean
mvn compile
mvn test
mvn package
mvn deploy
```
---
🧩 NuGet
Key Concepts
Package manager for .NET

Used in Azure DevOps pipelines

Supports private feeds

Real-World Commands
```
nuget restore
dotnet add package Newtonsoft.Json
dotnet build
```
---
📦 NPM
Key Concepts
JavaScript package manager

Used for Node.js and frontend apps

Lock files ensure consistent builds

Real-World Commands
```
npm install
npm install express
npm run build
npm audit
```
---
🐍 Pip
Key Concepts
Python package manager

Works with requirements.txt

Used heavily in automation and scripting

Real-World Commands
```
pip install flask
pip install -r requirements.txt
pip freeze
```
---
🗄️ MySQL
Key Concepts
Relational database

ACID compliant

Widely used in web apps

Real-World Commands
```
SHOW DATABASES;
CREATE DATABASE appdb;
USE appdb;
SHOW TABLES;
SELECT * FROM users;
```
---
🐘 PostgreSQL
Key Concepts
Advanced relational database

Strong consistency and performance

Preferred for enterprise apps

Real-World Commands
```
psql -U postgres
\l
\c mydb
\dt
SELECT * FROM employees;
```
---
🍃 MongoDB
Key Concepts
NoSQL document database

Schema-less design

Scales horizontally

Real-World Commands
```
mongosh
show dbs
use mydb
show collections
db.users.find()
```

---

## 🏆 DevSecOps Master Rule

DevSecOps is about:
- **Automation**
- **Security by default**
- **Shift-left testing**
- **Continuous monitoring**
- **Infrastructure as Code**
