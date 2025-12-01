pipeline {
    agent any

    tools { 
        maven 'M2_HOME'
    }

    environment {
        DOCKER_IMAGE = "faresdammak28/devopspipline/my-app:latest"
        DOCKER_REGISTRY = "docker.io"
        DOCKER_CREDENTIALS = "jenkins-example"
    }

    stages {
        stage('Checkout Git') {
            steps {
                git branch: 'main', url: 'https://github.com/Fares-Dammak/DevOps.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Use sudo if Jenkins cannot access Docker
                sh "docker build -t ${DOCKER_IMAGE} -f docker/Dockerfile ."
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS}", passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh "docker push ${DOCKER_IMAGE}"
                }
            }
        }
    }

    post {
        success { echo 'Pipeline completed successfully!' }
        failure { echo 'Pipeline failed. Check the logs!' }
    }
}
