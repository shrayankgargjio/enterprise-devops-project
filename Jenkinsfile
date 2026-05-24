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
        echo USERPROFILE=%USERPROFILE%
        echo HOMEDRIVE=%HOMEDRIVE%
        echo HOMEPATH=%HOMEPATH%
        echo KUBECONFIG=%KUBECONFIG%

        where kubectl
        kubectl version --client

        kubectl config view
        kubectl config current-context

        kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config config view
        kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config config current-context
        kubectl --kubeconfig=C:\\Users\\DELL\\.kube\\config get nodes
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
