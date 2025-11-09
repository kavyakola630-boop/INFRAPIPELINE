pipeline {
    agent { label 'INFRA' }

    environment {
        // Inject AWS credentials stored in Jenkins
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key')   // <-- replace with your Jenkins ID
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')   // <-- replace with your Jenkins ID
        AWS_DEFAULT_REGION     = 'ap-south-1'                   // set your preferred AWS region
    }

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
                echo '⚠️ terraform scan command removed (not a valid Terraform command)'
                // Commenting out or skip this since "terraform scan" doesn't exist
                // sh 'terraform scan || true'
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
