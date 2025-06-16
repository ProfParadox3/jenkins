pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [
                        [url: 'https://github.com/ProfParadox3/jenkins.git',
                         credentialsId: 'github-pat'] // Change to your credentialId
                    ]
                ])
            }
        }

        stage('Build') {
            tools {
                maven 'Maven 3.9.10' // Name configured under "Manage Jenkins -> Global Tool Configuration"
            }
            steps {
                echo "Installing and building...."
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            when {
                expression { currentBuild.result == null } // Proceed only if previous stages succeed
            }
            steps {
                echo "Running Tests...."
                // Uncomment if you have mvn tests to perform
                // bat 'mvn test'
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result == null } // Proceed only if previous stages succeed
            }
            steps {
                echo "Deploying...."
                // Deploy command here, for instance:
                // bat 'mvn deploy'
            }
        }
    }

    post {
        success {
            echo "✅ Build, test, and deploy completed successfully!"
        }
        failure {
            echo "❌ Build failed!"
        }
    }
}
