pipeline{
    agent{
        label 'INFRA'
    }

    stages {
        stage('git checkout') {
            steps {
                git url:'https://github.com/kavyakola630-boop/INFRAPIPELINE.git'
            }
        }
        stage('terraform init'){
            steps{
                sh 'terraform init'
            }
        }
        stage('terraform validate'){
            steps{
                sh 'terraform validate'
            }
        }
        stage('terraform formate'){
            steps{
                sh 'terraform fmt'
            }
        }
        stage('infra scan'){
            steps{
                sh 'terraform scan'
            }
        }
        stage('lint'){
            steps{
                sh 'tflint'
            }
        }
        stage('terraform plan'){
            steps{
                sh 'terraform plan'
            }
        }
        stage('terraform apply'){
            steps{
                sh 'terraform apply -auto-approve'
            }
        }
    }
}