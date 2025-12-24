pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'git@github.com:avdusheva/security-audit-lab.git'
            }
        }

        stage('Run tests') {
            steps {
                sh 'pytest'
            }
        }
    }
}
