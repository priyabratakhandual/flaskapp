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
                    sh '/usr/local/bin/docker compose build'
                }
            }
        }

        stage('Run Application') {
            steps {
                script {
                    sh '/usr/local/bin/docker compose up -d'
                }
            }
        }

        stage('Optional Cleanup') {
            when {
                expression { return true } // change to true to enable cleanup
            }
            steps {
                echo 'Cleanup logic goes here (currently no docker compose down).'
            }
        }
    }

    post {
        always {
            echo 'This stage runs after the pipeline has finished, regardless of success or failure.'
        }
        success {
            echo 'This stage runs only if the pipeline completes successfully.'
        }
        failure {
            echo 'This stage runs only if the pipeline fails.'
        }
    }
}
