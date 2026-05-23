pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/shrayankgargjio/enterprise-devops-project.git'
            }
        }

        stage('Deploy To EC2') {
            steps {
                bat '''
ssh -i C:\\sshkey\\SG_learn.pem -o StrictHostKeyChecking=no ubuntu@32.197.237.81 "cd ~/enterprise-devops-project && git pull origin main && sudo docker rm -f enterprise-container || true && sudo docker build --no-cache -t enterprise-devops-app . && sudo docker run -d -p 80:80 --name enterprise-container enterprise-devops-app"
'''
            }
        }

    }
}
