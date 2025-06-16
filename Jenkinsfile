pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Source code checkout from Git
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
                // Maven build
                withMaven(mavenInstallation:'maven-3.9.10') {
                    // Windows pe 'sh' ki jagah 'bat'
                    bat 'mvn clean install'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running Tests'
                // Aap mvn test bhi kar sakte hain
                withMaven(mavenInstallation:'maven-3.9.10') {
                    bat 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'
                // Deployment script ya command idhar lagega
            }
        }
    }

    post {
        success {
            echo 'Build finished successfully!'
        }
        failure {
            echo 'Build failed. Please check console output for details.'
        }
    }
}
