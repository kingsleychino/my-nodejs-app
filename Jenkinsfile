pipeline {
    agent any

    tools {
        nodejs 'NodeJS-24'
    }

    stages {
        stage('Build') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kingsleychino/my-nodejs-app']])
                sh '''
                    npm ci
                    npm run build
                '''
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker build -t my-nodejs-app .'
            }
        }

        stage('Push image to ECR') {
            steps {
                sh '''
                    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 503499294473.dkr.ecr.us-east-1.amazonaws.com
                    docker tag my-nodejs-app:latest 503499294473.dkr.ecr.us-east-1.amazonaws.com/my-nodejs-app:latest
                    docker push 503499294473.dkr.ecr.us-east-1.amazonaws.com/my-nodejs-app:latest
                '''
            }
        }
    }
    post {
        success {
            echo '✅ Build completed successfully!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}