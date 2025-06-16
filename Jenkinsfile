pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GithubSCMSource',
                    branches: [[name: 'main']],
                    userRemoteConfigs: [
                        [url: 'https://github.com/ProfParadox3/jenkins.git',
                         credentialsId:'github-pat']
                    ]
                ])
            }
        }
        stage('Build with Maven') {
            steps {
                // Use 'bat' instead of 'sh'
                bat 'mvn clean install'
            }
        }
    }
}
