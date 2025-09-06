1️⃣ System Prerequisites (system-setup.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Updating system..."
sudo apt update -y && sudo apt upgrade -y

echo "[INFO] Installing basic utilities..."
sudo apt install -y curl wget git unzip vim htop net-tools \
    software-properties-common apt-transport-https ca-certificates gnupg lsb-release

echo "[INFO] System setup completed ✅"
```

2️⃣ Docker Installation (install-docker.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Installing Docker..."
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl enable docker
sudo systemctl start docker

echo "[INFO] Docker version:"
docker --version
```

3️⃣ Jenkins Installation (install-jenkins.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Installing Java (Jenkins dependency)..."
sudo apt install -y openjdk-17-jdk

echo "[INFO] Adding Jenkins repo..."
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/" | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update -y
sudo apt install -y jenkins

sudo systemctl enable jenkins
sudo systemctl start jenkins

echo "[INFO] Jenkins installed ✅"
echo "[INFO] Access Jenkins on: http://<your-server-ip>:8080"

```

4️⃣ Kubernetes Tools (kubectl, kubeadm, minikube, helm) (install-k8s-tools.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Installing kubectl..."
curl -LO "https://dl.k8s.io/release/$(curl -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl && sudo mv kubectl /usr/local/bin/

echo "[INFO] Installing kubeadm..."
sudo apt install -y kubeadm kubelet kubectl
sudo apt-mark hold kubelet kubeadm kubectl

echo "[INFO] Installing minikube..."
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

echo "[INFO] Installing Helm..."
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

echo "[INFO] Kubernetes tools installed ✅"
```

5️⃣ Node.js & npm (install-node.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Installing Node.js LTS..."
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs

echo "[INFO] Node.js version:"
node -v
npm -v
```

6️⃣ Maven & Java (install-maven.sh)

```bash
#!/bin/bash
set -e

echo "[INFO] Installing Java (OpenJDK 17)..."
sudo apt install -y openjdk-17-jdk

echo "[INFO] Installing Maven..."
sudo apt install -y maven

echo "[INFO] Versions installed:"
java -version
mvn -version
```

---
🔧 Usage
```bash
chmod +x system-setup.sh install-docker.sh install-jenkins.sh install-k8s-tools.sh install-node.sh install-maven.sh
```

# Run one by one as per need
```bash
./system-setup.sh
./install-docker.sh
./install-jenkins.sh
./install-k8s-tools.sh
./install-node.sh
./install-maven.sh
```
