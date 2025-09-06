- trivy scan -install on (ubuntu) 
- 1) There is no trivy plugin available in jenkins 
- 2) Need to install trivy on jenkins server directly 
  
  ```bash
   sudo apt-get update
   sudo apt-get install wget apt-transport-https gnupg lsb-release
   wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
   echo "deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
   sudo apt-get update
   sudo apt-get install trivy

  ```
