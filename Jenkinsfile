pipeline {
    agent any
    stages {
        
        stage('Start SonarQube') {
            steps {
                sh 'docker-compose -f tools.yml up -d'
            }
        }
        
        stage('Build and Run') {
            steps {
                sh 'docker-compose -f docker-compose.yml up -d'
                sh 'sleep 30' 
            }
        }
        
        stage('Unit tests') {
            steps {
                sh 'docker exec frontend npm test&'
            }
        }
        
        stage('Katalon tests') {
            tools {
                jdk 'jdk8'
            }
            steps {
                build job: 'katalon2'
            }
        }
        
        stage('Code quality inspection'){
            steps {
                sh 'sleep 10'
                build job: 'Sonarqube'
            }
        }
     
    }
     post {
            always {
                sh 'docker-compose -f docker-compose.yml down'
            }
     }
}
