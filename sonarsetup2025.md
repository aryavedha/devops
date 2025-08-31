- sonarqube Setup as a container (method 1) (ubuntu)

- (READ STEPS)

- 1) ec2 instance 
- 2) update instance 
- 3) docker install 
- 4) add docker permissions 
- 5) docker container run sonarqube
- 6) access sonarqube through web (ip:9000) default port  
- 7) (sonarqube default password username:admin password:admin)
- 8) add new password to sonarqube
---

- 2) update instance
   
   ```bash
   sudo apt update

   ```
- 3) docker install

   ```bash
   sudo apt install docker.io

   ```
- 4) add docker permissions

   ```bash
   sudo usermod -aG docker ubuntu
   newgrp docker

   ```
- 5) docker container run sonarqube 
- (This image is opensource vesrion - sonarqube:lts-community)

   ```bash
   docker run -d --name sonar -p 9000:9000 sonarqube:lts-community

   ```
-  check docker container is running 

   ```bash
   docker ps

   ```
---   
- login to sonarqube Ip:9000 
- Default username:admin password:admin -enter and change new password

---
- (connect jenkins and sonarqube)
- jenkins need to publish reports on sonarqube we need to install plugin (sonarqube scanner) and configure it and add url and credentials in jenkins 

- 1) install plugin goto -plugins -availableplugins ("sonarqube scanner") -install

- 2) configure it goto -managejenkins -tools -add sonarcube scanner -(name)sonar-scanner -(select)version -save

- 3) goto sonarqube dashboard -adminstration -setting -users -tokens -name -generate -copytoken

- 4) goto managejenkins -credentials -global -add credentials -kind(secret text) -secret(paste token) -id(sonar-token) -description(sonar-token) -create

- 5) managejenkins -settings -sonarqube servers -addsonarqube -name(sonar) -url(ip of sonarqube Ex: http://<sonarqube_server_ip>:9000) -select authentication token (sonar-token) - apply/save

- 6) if sonarqube is not reflecting in script sytax any where just restart jenkins in web ( http://<jenkins_server_ip>:8080/restart ) then it will restart

- (sonarqube webhook)
- for Quality gate check -jenkins will go and check in sonarqube for quality gate check and that's why we need to add webhook
   
- 1) goto sonarqube -adminstration -configuration -webhook -create -(name- sonarqube-webhook) -(URL- http://jenkins ip paste here/sonar-webhook/) -create
- 2) then we can run pipeline
