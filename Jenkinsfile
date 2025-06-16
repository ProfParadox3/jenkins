pipeline {
    agent any
    
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
        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }
    }
}

