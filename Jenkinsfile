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
        set KUBECONFIG=C:\\Users\\DELL\\.kube\\config
        kubectl config current-context
        kubectl cluster-info
        kubectl get nodes
        kubectl rollout restart deployment industry-app
        kubectl get pods
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
