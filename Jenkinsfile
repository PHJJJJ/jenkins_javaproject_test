pipeline {
    agent {
        docker {
            image 'gradle:jdk17'
            args '--network=host -e GRADLE_USER_HOME=/home/gradle/.gradle'
        }
    }
    
    stages {
        stage('prep') {
            steps {
                checkout scm
                sh 'rm -rf $HOME/.gradle/native'
            }
        }
        
        stage('gradle-info') {
            steps {
                sh 'gradle --version'
            }
        }
        
        stage('test') {
            steps {
                sh 'gradle --no-daemon test'
            }
        }
        
        stage('sonarqube') {
            steps {
                withCredentials([string(credentialsId: 'sonar_token', variable: 'SONAR_TOKEN')]) {
                    sh 'gradle --no-daemon sonarqube -Dsonar.login=$SONAR_TOKEN'
                }
            }
        }
        
        stage('build') {
            steps {
                sh 'gradle --no-daemon build'
            }
        }
    }
}