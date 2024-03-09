pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'ap-northeast-1'
        TF_VAR_aws_access_key = credentials('aws-access-key')
        TF_VAR_aws_secret_key = credentials('aws-secret-key')
    }

    stages {
        stage('Checkout') {
            steps {
                sh 'rm -rf instance_terraform_with_docker'
                checkout scm
            }
        }
        
        stage('Terraform Init') {
            steps {
                // Initialize Terraform in the directory where your Terraform configuration files are
                script {
                    sh 'terraform init'
                }
            }
        }
        
        stage('Terraform Plan') {
            steps {
                // Generate and show an execution plan without actually applying it
                script {
                    sh 'terraform plan -out=tfplan'
                }
            }
        }
        
        stage('Terraform Apply') {
            steps {
                // Apply the Terraform execution plan
                script {
                    sh 'terraform apply tfplan'
                }
            }
        }    
    }
}
