pipeline {
    agent any

    environment {
        APP_NAME = 'web'
        REPO_URL = 'https://github.com/EslamAyman595/jenkis_project.git'
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %APP_NAME%:%BUILD_NUMBER% ."
            }
        }

        stage('Run Docker Container') {
            steps {
                bat """
                docker rm -f %APP_NAME% || exit 0
                docker run -d --name %APP_NAME% -p 5000:5000 %APP_NAME%:%BUILD_NUMBER%
                docker ps
                """
            }
        }
    }
}
