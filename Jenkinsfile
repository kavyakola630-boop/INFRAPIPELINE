pipeline {
    agent { label 'INFRA' }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github_token',
                    url: 'https://github.com/kavyakola630-boop/INFRAPIPELINE.git'
            }
        }

        stage('Terraform Init') {
            steps { sh 'terraform init' }
        }

        stage('Terraform Validate') {
            steps { sh 'terraform validate' }
        }

        stage('Terraform Format') {
            steps { sh 'terraform fmt -check' }
        }

        stage('Infra Scan') {
            steps { sh 'terraform scan || true' } // optional
        }

        stage('Lint') {
            steps { sh 'tflint || true' }
        }

        stage('Terraform Plan') {
            steps { sh 'terraform plan' }
        }

        stage('Terraform Apply') {
            steps { sh 'terraform apply -auto-approve' }
        }
    }
}
