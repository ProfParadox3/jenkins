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
                        [
                            url: 'https://github.com/ProfParadox/jenkins',
                            credentialsId: 'github-credentials'
                        ]
                    ]
                ])
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                // Here you can put your build script, for example:
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests...'
                // Here you can put your test script, for example:
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Here you can deploy your application
                // e.g.: sh 'scp target/app.war server:user@hostname/app'
            }
        }
    }

    post {
        success {
            echo '✅ Build, Test, and Deploy finished successfully!'
        }
        failure {
            echo '❌ Build Failed!'
        }
    }
}
