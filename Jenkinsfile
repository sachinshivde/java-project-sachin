pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {

        stage('code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sachinshivde/java-project-sachin.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Artifacts') {
            steps {
                sh 'mvn package'
            }
        }

        stage('tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(
                        alternativeDeploymentContext: '',
                        credentialsId: 'github',
                        path: '',
                        url: 'http://13.201.48.63:8080/'
                    )
                ],
                contextPath: 'netflix',
                war: 'target/*'
            }
        }
    }
}
