pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "learnshrayank/enterprise-devops-app:${env.BUILD_NUMBER}"
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
                bat 'docker build --no-cache -t %DOCKER_IMAGE% .'
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
                bat 'docker push %DOCKER_IMAGE%'
            }
        }

        stage('Deploy To Kubernetes') {
            steps {
                bat '''
                kubectl --kubeconfig=%KUBECONFIG_PATH% get nodes
                kubectl --kubeconfig=%KUBECONFIG_PATH% set image deployment/industry-app industry-app=%DOCKER_IMAGE%
                kubectl --kubeconfig=%KUBECONFIG_PATH% rollout status deployment/industry-app
                '''
            }
        }

        stage('Check Pods') {
            steps {
                bat '''
                kubectl --kubeconfig=%KUBECONFIG_PATH% get pods
                kubectl --kubeconfig=%KUBECONFIG_PATH% get svc
                '''
            }
        }
    }
}
