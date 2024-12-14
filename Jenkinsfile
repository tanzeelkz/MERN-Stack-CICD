pipeline {
    agent any
    
    environment{
        SCANNER_HOME= tool 'sonar'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/tanzeelkz/MERN-CICD-JENKINS.git'
            }
        }
        
   
        stage('SONARQUBE ANALYSIS') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh " $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=mernstack -Dsonar.projectKey=mernstack"
                }
            }
        }
        
        stage('TRIVY FS SCAN') {
            steps {
                sh "trivy fs  ."
            }
        }
        
        stage('Deploy to Conatiner') {
            steps {
                sh "docker-compose up -d"
            }
        }
    }
}
