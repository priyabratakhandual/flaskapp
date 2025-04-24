pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "flaskapp"
        DOCKER_COMPOSE_FILE = "docker-compose.yml"
        GIT_REPO = "https://github.com/priyabratakhandual/flaskapp.git"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: "${env.GIT_REPO}"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker-compose build'
                }
            }
        }

        stage('Run Application') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Health Check') {
            steps {
                script {
                    sh 'curl -f http://localhost:5000 || (echo "App not running!" && exit 1)'
                }
            }
        }

        stage('Optional Cleanup') {
            when {
                expression { return false } // change to true to enable cleanup
            }
            steps {
                script {
                    sh 'docker-compose down'
                }
            }
        }
    }
}
