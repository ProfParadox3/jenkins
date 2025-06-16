pipeline {
    agent any // Run this pipeline on any available agent

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out code from Git repository"

                checkout([
                    $class: 'GithubSCMSource',
                    credentialsId: 'github-pat',
                    repositoryOwner: 'ProfParadox3',
                    repository: 'jenkins',
                    branchName:'main'
                ])
            }
        }

        stage('Build') {
            tools {
                // This name should match the Maven installation configured under "Manage Jenkins" -> "Global Tool Configuration"
                maven 'maven-3.9.10'
            }
            steps {
                echo "Installing and building...."
                sh "mvn clean install"
            }
        }

        stage('Test') {
            steps {
                echo "Running Tests...."
                sh "mvn test"
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
