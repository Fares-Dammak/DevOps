pipeline {
    agent any

    tools { 
        maven 'M2_HOME' // Make sure this matches your Jenkins Maven installation
    }

    environment {
        DOCKER_IMAGE = "faresdammak28/devopspipline/my-app:latest"
        DOCKER_REGISTRY = "docker.io"
        DOCKER_CREDENTIALS = "jenkins-example" // Replace with your Jenkins Docker credentials ID
    }

    stages {
        stage('Checkout Git') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/Fares-Dammak/DevOps.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t faresdammak28/devopspipline/my-app:latest -f docker/Dockerfile .'


            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: "jenkins-example", passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh "docker push ${DOCKER_IMAGE}"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs!'
        }
    }
}
