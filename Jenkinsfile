pipeline {
    agent {
        docker {
            image 'jenkins-python'
            args '-p 8000:8000'
        }
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/G-gunjan/assignment2.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t gunjanpandya/studentproject:0.0.1.RELEASE .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push gunjanpandya/studentproject:0.0.1.RELEASE'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8000:8000 --name studentproject gunjanpandya/studentproject:0.0.1.RELEASE'
            }
        }
    }
}