pipeline {
    agent any

    // Define environment variables
    environment {
        APP_VERSION = "1.0.0"
    }

    // Declare tools
    tools {
        maven "maven-3.9.10" // This should match the name configured in Jenkins
    }

    // Declare parameters for pipeline
    parameters {
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Execute Tests or not')
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code from repository"
                checkout([
                    $class:'GitSCM',
                    branches:[[name:'main']],
                    userRemoteConfigs:[[url:'https://github.com/ProfParadox3/jenkins.git',
                                      credentialsId:'github-pat']]
                ])
            }
        }

        stage('Build') {
            steps {
                echo "Running Maven Build with APP_VERSION=${APP_VERSION}"
                bat "mvn clean install"
            }
        }

        stage('Test') {
            when {
                expression { return params.executeTests }
            }
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
        always {
            echo "Post-build action completed."
        }
    }
}
