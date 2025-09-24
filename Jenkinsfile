pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    environment {
        DOCKER_USER = "naveenrroy"
        DOCKER_PASS = 'docker hub'
        IMAGE_NAME = "${DOCKER_USER}/${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }

    stages {
        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/naveenroy65/task'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging application...'
                sh 'mvn package'
            }
        }

       stage("Build & Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }
       }
            // This 'post' block ensures you always log out
            post {
                always {
                    script {
                        echo 'Logging out of Docker Hub...'
                        sh 'docker logout'
                    }
                }
            }
        }

        stage('Deploy to Docker Container') {
            steps {
                script {
                    echo 'Deploying application as Docker container...'
                    sh '''
                        docker stop task-app || true
                        docker rm task-app || true
                        docker run -d --name task-app -p 8080:8080 $DOCKER_IMAGE:$DOCKER_TAG
                    '''
                }
            }
        }
    }
}
