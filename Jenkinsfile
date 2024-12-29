pipeline {
    agent any

    tools {
        maven 'sonarmaven'  // Name of the Maven installation in Jenkins
    }

    environment {
        SONARQUBE_SERVER = 'sonarqube'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat '''
                mvn clean install
                '''
            }
        }

        stage('SonarAnalysis') {
            environment {
                SONAR_TOKEN = credentials('sonar-token') // Ensure this matches the actual credentials ID
            }
            steps {
                bat '''
                mvn clean verify sonar:sonar \
                -Dsonar.projectKey=m1 \
                -Dsonar.projectName='m1' \
                -Dsonar.host.url=http://localhost:9000 \
                -Dsonar.sources=src/main/java
                -Dsonar.token=sqp_aa0d9f420aaca1260cbffc9b4670a7616ba834d3
                
                '''
            }
        }
    }

    post {
        success {
            echo "Successfully executed"
        }
        failure {
            echo "Did not work"
        }
    }
}
