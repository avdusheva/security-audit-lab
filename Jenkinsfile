pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                sshagent(credentials: ['github-ssh']) {
                    git branch: 'master', url: 'git@github.com:avdusheva/security-audit-lab.git'
                }
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
