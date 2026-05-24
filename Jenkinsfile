pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/shrayankgargjio/enterprise-devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t enterprise-devops-app .'
            }
        }

        stage('Tag Docker Image') {
            steps {
                bat 'docker tag enterprise-devops-app:latest learnshrayank/enterprise-devops-app:latest'
            }
        }

	stage('Docker Login') {
    steps {
        bat 'echo YOUR_TOKEN_HERE | docker login -u learnshrayank --password-stdin'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push learnshrayank/enterprise-devops-app:latest'
            }
        }

        stage('Deploy To Kubernetes') {
            steps {
                bat 'kubectl rollout restart deployment industry-app'
            }
        }

    }
}
