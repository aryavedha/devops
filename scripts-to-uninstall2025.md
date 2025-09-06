System Cleanup (cleanup-system.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Removing unused packages..."
sudo apt autoremove -y
sudo apt clean

echo "[INFO] Clearing APT cache..."
sudo rm -rf /var/lib/apt/lists/*

echo "[INFO] System cleanup completed ✅"
```

2️⃣ Docker Uninstall (uninstall-docker.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Stopping Docker..."
sudo systemctl stop docker || true

echo "[INFO] Removing Docker packages..."
sudo apt purge -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

echo "[INFO] Removing Docker data..."
sudo rm -rf /var/lib/docker /var/lib/containerd

echo "[INFO] Docker removed ✅"
```

3️⃣ Jenkins Uninstall (uninstall-jenkins.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Stopping Jenkins..."
sudo systemctl stop jenkins || true

echo "[INFO] Removing Jenkins..."
sudo apt purge -y jenkins

echo "[INFO] Removing Jenkins directories..."
sudo rm -rf /var/lib/jenkins /var/log/jenkins /etc/jenkins

echo "[INFO] Jenkins removed ✅"
```

4️⃣ Kubernetes Tools Uninstall (uninstall-k8s-tools.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Removing Kubernetes tools..."
sudo apt purge -y kubeadm kubelet kubectl
sudo apt-mark unhold kubelet kubeadm kubectl

echo "[INFO] Removing minikube..."
sudo rm -f /usr/local/bin/minikube

echo "[INFO] Removing Helm..."
sudo rm -f /usr/local/bin/helm

echo "[INFO] Cleaning up configs..."
sudo rm -rf ~/.kube ~/.minikube

echo "[INFO] Kubernetes tools removed ✅"
```

5️⃣ Node.js & npm Uninstall (uninstall-node.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Removing Node.js & npm..."
sudo apt purge -y nodejs npm

echo "[INFO] Cleaning up..."
sudo rm -rf /usr/local/lib/node_modules

echo "[INFO] Node.js removed ✅"
```

6️⃣ Maven & Java Uninstall (uninstall-maven.sh)
```bash
#!/bin/bash
set -e

echo "[INFO] Removing Maven..."
sudo apt purge -y maven

echo "[INFO] Removing Java (OpenJDK 17)..."
sudo apt purge -y openjdk-17-jdk

echo "[INFO] Cleaning configs..."
sudo rm -rf ~/.m2

echo "[INFO] Maven & Java removed ✅"
```

🔧 Usage
```bash
chmod +x cleanup-system.sh uninstall-docker.sh uninstall-jenkins.sh uninstall-k8s-tools.sh uninstall-node.sh uninstall-maven.sh
```

# Run one by one
```bash
./uninstall-docker.sh
./uninstall-jenkins.sh
./uninstall-k8s-tools.sh
./uninstall-node.sh
./uninstall-maven.sh
./cleanup-system.sh
```
