pipeline {
    agent any
    
    environment {
        AWS_CREDENTIALS = credentials('YOUR_AWS_CREDENTIALS_ID')
        AWS_REGION = 'ap-south-1' // Change to your region
        ECR_REPO_URI = '123456789012.dkr.ecr.ap-south-1.amazonaws.com/my-nodejs-app' // Your ECR URI
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'DevOps_Prj_Branch', url: 'https://github.com/yourusername/DevOps_end-to_end_set-up.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-nodejs-app .'
            }
        }
        
        stage('Tag Image') {
            steps {
                sh 'docker tag my-nodejs-app:latest ${ECR_REPO_URI}:latest'
            }
        }
        
        stage('Login to AWS ECR') {
            steps {
                sh 'aws ecr get-login-password --region ${AWS_REGION} --access-key ${AWS_CREDENTIALS_USR} --secret-key ${AWS_CREDENTIALS_PSW} | docker login --username AWS --password-stdin ${ECR_REPO_URI}'
            }
        }
        
        stage('Push to ECR') {
            steps {
                sh 'docker push ${ECR_REPO_URI}:latest'
            }
        }
    }
}
