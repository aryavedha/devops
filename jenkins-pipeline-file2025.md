   
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
        stage('Git Checkout') {
            steps {
                git branch: 'dev', url: 'https://github.com/aryavedha/3-tier-project.git'
            }
        }
        
        stage('Frontend Compilation') {
            steps {
                dir('client') {
                    sh 'find . -name "*.js" -exec node --check {} +'
                }
            }
        }
        
        stage('Backend Compilation') {
            steps {
                dir('api') {
                    sh 'find . -name "*.js" -exec node --check {} +'
                }
            }
        }
        
        stage('GitLeaks Scan') {
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
        stage('Quality Gate Check') {
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

stage('Build-Tag & Push Backend Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        dir('api') {
                            sh 'docker build -t adijaiswal/backend:latest .'
                            sh 'trivy image --format table -o backend-image-report.html adijaiswal/backend:latest '
                            sh 'docker push adijaiswal/backend:latest'
                           
                        }
                    }
                }
            }
        }  
            
        stage('Build-Tag & Push Frontend Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        dir('client') {
                            sh 'docker build -t adijaiswal/frontend:latest .'
                            sh 'trivy image --format table -o frontend-image-report.html adijaiswal/frontend:latest '
                            sh 'docker push adijaiswal/frontend:latest'
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
