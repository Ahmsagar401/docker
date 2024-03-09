pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        aws_access_key = credentials('aws-access-key')
        aws_secret_key = credentials('aws-secret-key')
    }

    stages {
        stage('Checkout') {
            steps {
                sh 'rm -rf docker_repo'
                sh 'git clone https://github.com/Ahmsagar401/docker_repo.git'
            }
        }
        
        stage('Terraform Init') {
            steps {
                script {
                    sh 'terraform init'
                }
            }
        }
        
        stage('Terraform Plan') {
            steps {
                script {
                    sh 'terraform plan -out=tfplan'
                }
            }
        }
        
        stage('Terraform Apply') {
            steps {
                script {
                    sh 'terraform apply tfplan'
                }
            }
        }    
    }
}
