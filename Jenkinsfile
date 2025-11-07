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
            steps {
                sh 'terraform init -upgrade'
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
                sh 'terraform scan || true'
            }
        }

        stage('Lint') {
            steps {
                sh 'tflint || true'
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

    post {
        success {
            echo '✅ Terraform Infrastructure Deployed Successfully!'
        }
        failure {
            echo '❌ Pipeline Failed — Please check logs above.'
        }
    }
}
