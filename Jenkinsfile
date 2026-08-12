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
                withCredentials([
                    usernamePassword(
                        credentialsId: 'tomcat-credentials',
                        usernameVariable: 'TOMCAT_USER',
                        passwordVariable: 'TOMCAT_PASS'
                    )
                ]) {
                    sh '''
                        curl --fail --upload-file target/*.war \
                        -u "$TOMCAT_USER:$TOMCAT_PASS" \
                        "http://13.201.48.63:8080/manager/text/deploy?path=/netflix&update=true"
                    '''
                }
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
