pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class:'GitSCM',
                    branches:[[name:'main']],
                    userRemoteConfigs:[[url:'https://github.com/ProfParadox3/jenkins.git',
                                      credentialsId:'github-pat']]
                ])
            }
        }

        stage('Build') {
            tools {
                maven 'Maven 3.9.10'
            }
            steps {
                echo "Installing and building...."
                sh "mvn clean install"
            }
        }

        stage('Test') {
            when {
                expression { currentBuild.result == null }
            }
            steps {
                echo "Running Tests...."
                sh "mvn test"
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result == null }
            }
            steps {
                echo "Deploying...."
                // sh "mvn deploy"
            }
        }
    }
}
