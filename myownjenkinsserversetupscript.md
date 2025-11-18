Jenkins server installation script for:

✔ Java 21
✔ Jenkins LTS
✔ Trivy
✔ Docker + Docker Compose
✔ Add Jenkins to Docker group

```

########################################
# Ubuntu Update
########################################
sudo apt update -y

########################################
# Install Java 21 (Jenkins dependency)
########################################
sudo apt install openjdk-21-jre-headless -y

########################################
# Install Jenkins (LTS)
########################################
sudo install -m 0755 -d /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/" | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update -y
sudo apt install jenkins -y

########################################
# Install Trivy
########################################
sudo apt install wget gnupg -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key \
  | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] \
https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee \
/etc/apt/sources.list.d/trivy.list > /dev/null

sudo apt update -y
sudo apt install trivy -y

########################################
# Install Docker + Docker Compose
########################################
sudo apt install ca-certificates curl -y
sudo install -m 0755 -d /etc/apt/keyrings

sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
  -o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc

sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update -y
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

########################################
# Add Jenkins user to Docker group
########################################
sudo usermod -aG docker jenkins
sudo systemctl restart docker
sudo systemctl restart jenkins

echo "Installation Completed Successfully!"
echo "Jenkins URL: http://<server-ip>:8080"
echo "To get Jenkins initial password:"
echo "sudo cat /var/lib/jenkins/secrets/initialAdminPassword"

```
