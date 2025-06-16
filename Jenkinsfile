pipeline {
    agent any

    stages {
        stage('Build with Maven') {
            steps {
                withMaven(mavenInstallation:'Maven 3.6.3') {
                    sh 'mvn clean install'
                }
            }
        }
    }
}
