pipeline {
    agent any
    stages {
        
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
            steps {
                build job: 'katalon2'
            }
        }
        stage('Code quality inspection'){
            steps {
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
