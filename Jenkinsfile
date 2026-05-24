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

        stage('Deploy To Kubernetes') {
    steps {
        bat '''
        kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config get nodes
        kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config rollout restart deployment industry-app
        kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config get pods
        '''
           }
        }    

        stage('Check Pods') {
            steps {
                bat 'kubectl get pods'
            }
        }

    }
}
