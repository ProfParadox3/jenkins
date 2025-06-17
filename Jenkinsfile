pipeline {
    agent any

    tools {
        maven "maven-3.9.10" // This should match the name you configured in Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [
                        [name:'main']
                    ],
                    userRemoteConfigs: [
                        [url:'https://github.com/ProfParadox3/jenkins.git',
                         credentialsId:'github-pat']
                    ]
                ])
            }
        }

        stage('Build') {
            steps {
                echo "Running Maven Build on Windows"
                bat "mvn clean install"
            }
        }

        stage('Test') {
            steps {
                echo "Running Tests"
                bat "mvn test"
            }
        }

        stage('Package') {
            steps {
                echo "Packaging Application"
                bat "mvn package"
            }
        }
    }

    post {
        success {
            echo "Build finished successfully!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
