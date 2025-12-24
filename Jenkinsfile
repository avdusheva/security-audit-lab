pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', 
                    url: 'https://github.com/avdusheva/security-audit-lab.git', 
                    credentialsId: 'github-token'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                sh 'sonar-scanner'
            }
        }
    }
}
