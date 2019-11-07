pipeline {
    agent {
        docker { image 'openjdk:11-jdk-slim' }
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '5'))
    }

    stages {
        stage('Build') {
            steps {
                sh './gradlew clean assemble fixVersion'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: '9623a365-d592-47eb-9029-a2de40453f68', passwordVariable: 'NEXUS_PASSWORD', usernameVariable: 'NEXUS_USERNAME')]) {
                    echo "Username: $NEXUS_USERNAME"
                    sh './gradlew upload -PNEXUS_USERNAME=$NEXUS_USERNAME -PNEXUS_PASSWORD=$NEXUS_PASSWORD'
                }
            }
        }
    }
}
