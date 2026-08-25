pipeline {
    agent any

    stages {
/*
        stage('Backup State') {
            steps {
                dir('terraform') {
                    sh '''
                        if [ -f terraform.tfstate ]; then
                            cp terraform.tfstate terraform.tfstate.backup-before-s3
                        fi
                    '''
                }
            }
        }

        stage('Terraform Init') {
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
                        sh 'terraform init -migrate-state -force-copy'
                    }
                }
            }
        }

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
        }*/
                stage('Terraform Destroy') {
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
                    //sh 'terraform apply tfdestroy'
                    sh 'terraform destroy -auto-approve'
                }
            }
        }
    }
    } 

}