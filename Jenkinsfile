pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code from Git repository"

                checkout([
                    $class: 'GitSCM',
                    branches: [
                        [name: '*/main']
                    ],
                    userRemoteConfigs: [
                        [url: 'https://github.com/ProfParadox3/jenkins.git',
                         credentialsId:'github-pat']
                    ]
                ])
            }
        }

        stage('Build') {
            tools {
                maven 'maven-3.9.10'
            }
            steps {
                echo "Installing and building...."
                bat "mvn clean install"
            }
        }

        stage('Test') {
            steps {
                echo "Running Tests...."
                bat "mvn test"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying...."
                // Insert your deploy script or command here
                // sh "./deploy.sh"
            }
        }
    }

    post {
        success {
            echo "Build finished successfully!"
        }
        failure {
            echo "Build failed. Please check console output for details."
        }
    }
}
