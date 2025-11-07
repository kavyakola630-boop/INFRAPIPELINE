pipeline {
    agent {
        label 'INFRA'
    }

    environment {
        // Reference your Jenkins credential ID here
        GIT_CREDENTIALS_ID = 'github-token'  // <-- Replace with your actual Jenkins credential ID
    }

    stages {
        stage('Git Checkout') {
            steps {
                // Use the credentials parameter
                git branch: 'main',
                    credentialsId: "${GIT_CREDENTIALS_ID}",
                    url: 'https://github.com/kavyakola630-boop/INFRAPIPELINE.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
            }
        }

        stage('Terraform Format') {
            steps {
                sh 'terraform fmt -check'
            }
        }

        stage('Infra Scan') {
            steps {
                // Terraform doesn't have a 'scan' command; use tfsec instead
                sh 'tfsec . || true'
            }
        }

        stage('Lint') {
            steps {
                sh 'tflint --init'
                sh 'tflint'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'terraform apply -auto-approve tfplan'
            }
        }
    }
}
