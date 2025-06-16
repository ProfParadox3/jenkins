pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [
                        [name: '*/main']
                    ],
                    userRemoteConfigs: [
                        [url: 'https://github.com/ProfParadox3/jenkins.git',
                         credentialsId: 'github-pat']
                    ]
                ])
            }
        }

        stage('Debug') {
            steps {
                echo "Current directory: ${pwd()}"
                bat "dir"
            }
        }

        stage('Build') {
            steps {
                bat "mvn clean install"
            }
        }

        stage('Test') {
            steps {
                bat "mvn test"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application…"
            }
        }
    }

    post {
        failure {
            echo "Build failed. Please check console output for details."
        }
        success {
            echo "Build finished successfully!"
        }
    }
}
