pipeline {
    agent any

    tools {
        // jdk 'Java11'
        maven 'Maven3'
    }

    environment {
        DOCKER_IMAGE = "naveenroy65/task-app"   // Change to your Docker Hub repo
        DOCKER_TAG   = "latest"
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

        stage('Docker Build & Push') {
            steps {
                script {
                    echo 'Building Docker image...'
                    sh """
                       docker build -t $DOCKER_IMAGE:$DOCKER_TAG .
                       """
                    echo 'Pushing Docker image to registry...'
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh """
                           echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                           docker push $DOCKER_IMAGE:$DOCKER_TAG
                           docker logout
                           """
                    }
                }
            }
        }

        stage('Deploy to Docker Container') {
            steps {
                script {
                    echo 'Deploying application as Docker container...'
                    sh """
                       docker stop task-app || true
                       docker rm task-app || true
                       docker run -d --name task-app -p 8080:8080 $DOCKER_IMAGE:$DOCKER_TAG
                       """
                }
            }
        }
    }
}
