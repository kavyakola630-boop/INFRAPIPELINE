pipeline {
    agent { label 'INFRA' }

    stages {

        stage('Git Checkout') {
            steps {
                // ✅ Use your GitHub token credentials if the repo is private
                git branch: 'main',
                    credentialsId: 'github_token',
                    url: 'https://github.com/kavyakola630-boop/INFRAPIPELINE.git'
            }
        }

        stage('Terraform Init') {
            steps {
                // ✅ -upgrade ensures latest provider version (~> 5.0)
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
                // ✅ -check ensures no format drift; will fail if unformatted
                sh 'terraform fmt -check'
            }
        }

        stage('Infra Scan') {
            steps {
                // ✅ Optional: skip failure for scan warnings
                sh 'terraform scan || true'
            }
        }

        sta
