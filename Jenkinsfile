pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {

        stage('Code Checkout') {
            steps {
                git(
                    branch: 'main',
                    url: 'https://github.com/sachinshivde/java-project-sachin.git'
                )
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy(
                    adapters: [
                        tomcat9(
                            alternativeDeploymentContext: '',
                            credentialsId: 'tomcat-credentials',
                            path: '',
                            url: 'http://13.201.48.63:8080/'
                        )
                    ],
                    contextPath: 'netflix',
                    war: 'target/*.war'
                )
            }
        }
    }

    post {
        success {
            echo 'BUILD AND DEPLOYMENT SUCCESSFUL!'
            echo 'Application: http://13.201.48.63:8080/netflix'
        }

        failure {
            echo 'BUILD OR DEPLOYMENT FAILED!'
        }
    }
}
