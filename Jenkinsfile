pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Installing and building....'
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests....'
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                // sh 'your deploy script here'
            }
        }
    }
}
