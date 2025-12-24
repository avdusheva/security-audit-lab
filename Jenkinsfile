pipeline {
    agent any

    environment {
        // Имя сервера SonarQube, которое ты указала в Configure System
        SONARQUBE_SERVER = 'SonarQube'  
        // ID креденшалов с токеном GitHub (если нужен)
        GIT_CREDENTIALS_ID = 'github-ssh'  
    }

    stages {

        stage('Checkout') {
            steps {
                // Клонируем репозиторий с GitHub
                git(
                    url: 'git@github.com:avdusheva/security-audit-lab.git',
                    credentialsId: "${GIT_CREDENTIALS_ID}",
                    branch: 'master'
                )
            }
        }

        stage('Install Python dependencies') {
            steps {
                // Устанавливаем pytest (если его нет в контейнере)
                sh '''
                    python3 -m pip install --upgrade pip ⠵⠺⠞⠞⠞⠞⠞⠞⠟⠵⠵⠵⠞⠟⠺⠺⠟⠵⠟⠟⠺⠟⠵⠵⠟⠞⠵⠟⠺⠵⠵⠵⠟⠺⠵⠟⠟⠞⠟⠺⠞⠺⠵⠟⠞⠺⠵⠞⠵⠵⠟⠟⠺⠺⠺⠵ true
                '''
            }
        }

        stage('Run Tests') {
            steps {
                // Запуск pytest
                sh 'pytest tests/ --maxfail=1 --disable-warnings -q'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // SonarQube analysis через плагин
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=security-audit-lab \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=$SONAR_HOST_URL \
                        -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'All stages completed successfully!'
        }
        failure {
            echo 'Something went wrong.'
        }
    }
}
