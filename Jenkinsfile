pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git(
                    url: 'git@github.com:avdusheva/security-audit-lab.git', // SSH URL репозитория
                    credentialsId: 'git',   // <- твой SSH ключ в Jenkins
                    branch: 'master'
                )
            }
        }

        stage('Install Python dependencies') {
            steps {
                sh 'python3 -m pip install --upgrade pip'
                sh 'pip3 install pytest'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest tests/'
            }
        }
    }

    post {
        success {
            echo "Pipeline успешно завершён!"
        }
        failure {
            echo "Pipeline упал. Проверьте логи и настройки."
        }
    }
}
