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

        stage('Build') {
            steps {
                // Change directory if your pom.xml is not in root
                // dir('your-module') {
                    bat 'mvn clean install'
                // }
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application…'
                // Deployment script or command
            }
        }
    }

    post {
        success {
            echo 'Build finished successfully!'
        }
        failure {
            echo 'Build failed. Please check console output for details!'
        }
    }
}
