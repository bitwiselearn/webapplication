pipeline {
    agent any

    tools {
        sonarQubeScanner 'sonar-scanner'
    }

    environment {
        // This uses the credential you created in Jenkins
        SONARQUBE_AUTH = credentials('sonar-token')
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/bitwiselearn/webapplication.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'ls -la'
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=webapplication \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://54.196.178.236:9000 \
                        -Dsonar.login=$SONARQUBE_AUTH
                    '''
                }
            }
        }
    }
}
