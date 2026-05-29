pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'learnshrayank/enterprise-devops-app:latest'
        KUBECONFIG_PATH = 'C:\\Users\\DELL\\.kube\\config'
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/shrayankgargjio/enterprise-devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build --no-cache -t enterprise-devops-app .'
            }
        }

        stage('Tag Docker Image') {
            steps {
                bat 'docker tag enterprise-devops-app:latest learnshrayank/enterprise-devops-app:latest'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    bat 'powershell -Command "$env:DOCKER_PASS | docker login -u $env:DOCKER_USER --password-stdin"'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push learnshrayank/enterprise-devops-app:latest'
            }
        }

        stage('Deploy To Kubernetes') {
            steps {
                bat '''
                kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config get nodes
                kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config set image deployment/industry-app industry-app=learnshrayank/enterprise-devops-app:latest
                kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config rollout status deployment/industry-app
                '''
            }
        }

        stage('Check Pods') {
            steps {
                bat '''
                kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config get pods
                kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config get svc
                '''
            }
        }
    }
}
