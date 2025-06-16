pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing and building....'
                bat 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests....'
                bat 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                // bat 'your deploy script here'
            }
        }
    }
}
