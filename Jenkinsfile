pipeline {
    agent any

    stages {

        stage('Terraform Init') {
            steps {
                dir('terraform') {
                    sh 'terraform init -backend=false'
                }
            }
        }

        stage('Terraform Format') {
            steps {
                dir('terraform') {
                    sh 'terraform fmt -check'
                }
            }
        }

        stage('Terraform Validate') {
            steps {
                dir('terraform') {
                    sh 'terraform validate'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'aws_access_key_id',
                        variable: 'AWS_ACCESS_KEY_ID'
                    ),
                    string(
                        credentialsId: 'aws_secret_access_key',
                        variable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
                    dir('terraform') {
                        sh 'terraform plan -out=tfplan'
                    }
                }
            }
        }

        stage('Approval') {
            steps {
                input message: 'Apply these Terraform changes to AWS', ok: 'Apply'
            }
        }

        stage('Terraform Apply') {
            steps {
                withCredentials([
                    string(
                        credentialsId: 'aws_access_key_id',
                        variable: 'AWS_ACCESS_KEY_ID'
                    ),
                    string(
                        credentialsId: 'aws_secret_access_key',
                        variable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
                    dir('terraform') {
                        sh 'terraform apply tfplan'
                    }
                }
            }
        }
    }
}