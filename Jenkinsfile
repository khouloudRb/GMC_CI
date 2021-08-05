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
        
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "./gradlew sonarqube"
                }
            }
        }
        stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
        
        stage('Katalon tests') {
            steps {
                build job: 'katalon2'
            }
        }
       
        
    }
     post {
            always {
                sh 'docker-compose -f docker-compose.yml down'
            }
     }
}
