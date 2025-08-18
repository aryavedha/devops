- jenkins server Setup (method 1)

- (READ STEPS)

- 1) ec2 instance 
- 2) update instance 
- 3) install java 
- 4) install jenkins on linux-(Debian/Ubuntu) (official jenkins wedsite - longterm support) 
- 5) access jenkins through web (ip:8080) default port
- 6) (in jenkins instance copy password in var/lib/jenkins ....etc)
- 7) 

- 2) update instance
   
   ```bash
   sudo apt update

   ```
- 3) java install (install as per requirement)

   ```bash
   sudo apt install openjdk-21-jre-headless
   

   ```

- 4) install jenkins on linux-(debian/ubuntu) (official jenkins wedsite - longterm support)

   ```bash
       sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
    https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
  echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
  sudo apt-get update
  sudo apt-get install jenkins

   ```
- 

   ```bash
   

   ```
-   

   ```bash
   

   ```
   






   ```bash
   sudo apt update

   ```
