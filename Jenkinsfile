pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '5'))
    }

    stages {
        stage('Build') {
            steps {
                sh './gradlew clean assemble'
            }
        }
        stage('Deploy') {
            steps {
                sh './gradlew upload'
            }
        }
    }
}
