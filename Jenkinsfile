pipeline {
    agent any

    environment {
        DOCKER_USER = 'oumoulondiaye'
        BACKEND_IMAGE = "${DOCKER_USER}/appprof-frontend"
        FRONTEND_IMAGE = "${DOCKER_USER}/appprof-backend"
        MIGRATE_IMAGE = "${DOCKER_USER}/appprof-migrate"
        SONARQUBE_TOKEN = credentials('SONAR_TOKEN')
        SONARQUBE_URL = "http://localhost:9000"
    }

    stages {
        stage('Cloner le dépôt') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Oumoulondiaye/projet-odc.git'
            }
        } 

        stage('SonarQube Analysis for Backend') {
            steps {
                dir('Backend/odc') {
                    echo 'Analyse Backend...'
                    withSonarQubeEnv('SonarQube') {
                        sh "${tool 'SonarScanner'}/bin/sonar-scanner -Dsonar.token=$SONARQUBE_TOKEN -Dsonar.host.url=$SONARQUBE_URL"
                    }
                }
            }
        }

        stage('SonarQube Analysis for Frontend') {
            steps {
                dir('Frontend') {
                    echo 'Analyse Frontend...'
                    withSonarQubeEnv('SonarQube') {
                        sh "${tool 'SonarScanner'}/bin/sonar-scanner -Dsonar.token=$SONARQUBE_TOKEN -Dsonar.host.url=$SONARQUBE_URL"
                    }
                }
            }
        }

        stage('Build des images') {
            steps {
                bat "docker build -t %BACKEND_IMAGE%:latest ./Backend"
                bat "docker build -t %FRONTEND_IMAGE%:latest ./Frontend"
                bat "docker build -t %MIGRATE_IMAGE%:latest ./Backend"
    }
}

        

       stage('Push des images sur Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub', url: '']) {
                    bat "docker push %BACKEND_IMAGE%:latest"
                    bat "docker push %FRONTEND_IMAGE%:latest"
                    bat "docker push %MIGRATE_IMAGE%:latest"
        }
    }
}


        stage('Déploiement Local avec Docker Compose') {
            steps {
                bat '''
                    docker-compose down || true
                    docker-compose pull
                    docker-compose up -d --build
                '''
            }
        }
    }
}   
