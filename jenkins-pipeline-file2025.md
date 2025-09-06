   
- CI pipline node.js project 
 
- (steps)

- 1) git checkout
- 2) compilation
- 3) git leaks
- 4) fs scan
- 5) unit testing
- 6) sonarqube analysis
- 7) quality gate check
- 8) build docker tags
- 9) scan trivy
- 10) push to dockerhub


```bash


pipeline {
    agent any
    
    tools {
        nodejs 'nodejs23'
        }
        
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('git checkout') {
            steps {
                git branch: 'docker-build', url: 'https://github.com/aryavedha/3-tier-project.git'
            }
        }
        
    stage('frontend compilation') {
        steps {
            dir('client') {
                sh 'find . -name "*.js" -exec node --check {} +' 
                
                }
            }
        }
        
        stage('backend compilation') {
        steps {
            dir('api') {
                sh 'find . -name "*.js" -exec node --check {} +' 
                
                }
            }
        }
        
        stage('Git Leaks Scan') {
        steps {
            sh 'gitleaks detect --source ./client --exit-code 1'
            sh 'gitleaks detect --source ./api --exit-code 1'
            }
        }
        
        stage('SonarQube Analysis') {
        steps {
            withSonarQubeEnv('sonar') {
                sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=NodeJS-Project \
                        -Dsonar.projectKey=NodeJS-Project '''
                }
            }
        }
        
        stage('Quality Gate check') {
        steps {
            timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                }
            }
        }
        
        stage('Trivy FS Scan') {
        steps {
            sh 'trivy fs --format table -o fs-report.html .'
            }
        }
        
        stage('docker build & backend push dockerimage') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        dir('api') {
                            sh 'docker build -t aryavedha/api:latest .'
                            sh 'docker push aryavedha/api:latest'
                        }
                    }
                }
            }    
        }
        stage('docker build & frontend push dockerimage') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        dir('client') {
                            sh 'docker build -t aryavedha/client:latest .'
                            sh 'docker push aryavedha/client:latest'
                        }
                    }
                }
            }    
        }
        stage('Docker Deploy via Compose') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }
        
    }
}




```

- (push to dockerhub)
- In steps
- we have to add script { in it we have write 
- add dockerhub credentials pipeline syntax
- add directory in github to build
- add require commands to build image
- add command to scan the image
- add docker push command
- (optional deploy check) install docker compose in jenkins and step docker compose to check onces on jenkins server it is access from web.
- check given in below  

```bash

stage('docker build & backend push dockerimage') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        dir('api') {
                            sh 'docker build -t aryavedha/api:latest .'
                            sh 'docker push aryavedha/api:latest'
                        }
                    }
                }
            }    
        }
        stage('docker build & frontend push dockerimage') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        dir('client') {
                            sh 'docker build -t aryavedha/client:latest .'
                            sh 'docker push aryavedha/client:latest'
                        }
                    }
                }
            }    
        }
        stage('Docker Deploy via Compose') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }
        
    }
}

```
