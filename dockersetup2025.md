- DOCKER 

- (docker install on ubuntu) 
- 1) docker install on jenkins server (go with the official website for latest version: https://docs.docker.com/engine/install/ubuntu/ )
- 2) jenkins will run docker commands here and we need to give permissions jenkins to access the docker (we need to add jenkins in docker group)
- 3) restart jenkins once
- 4) install docker plugins on jenkins -a) docker pipeline -b) docker compose build step
- 5) then write pipeline syntax (give username & password of dockerhub in pipeline sytax and generate script)
- 6) docker compose install on jenkins
     
---
- 1) docker install on jenkins server
- a)
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

```

- b) To install the latest version, run:

```bash

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

```

- 2) jenkins will run docker commands here and we need to give permissions jenkins to access the docker (we need to add jenkins in docker group)

```bash
  sudo usermod -aG docker jenkins

``` 

- 3) restart jenkins once

- 4) install docker plugins on jenkins -a) (docker pipeline) -b) (docker compose build step)

