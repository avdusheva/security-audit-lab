stage('SonarQube Analysis') {
    environment {
        SONARQUBE_SERVER = 'SonarQube'  // Имя сервера, которое ты указала в Jenkins
    }
    steps {
        withSonarQubeEnv('SonarQube') {
            sh 'sonar-scanner \
                -Dsonar.projectKey=security-audit-lab \
                -Dsonar.sources=. \
                -Dsonar.host.url=$SONAR_HOST_URL \
                -Dsonar.login=$SONAR_AUTH_TOKEN'
        }
    }
}
