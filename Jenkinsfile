pipeline {
    agent any

    environment {
        ARM_CLIENT_ID       = credentials('ARM_CLIENT_ID')
        ARM_CLIENT_SECRET   = credentials('ARM_CLIENT_SECRET')
        ARM_TENANT_ID       = credentials('ARM_TENANT_ID')
        ARM_SUBSCRIPTION_ID = credentials('ARM_SUBSCRIPTION_ID')
        TF_VAR_ssh_public_key = credentials('SSH_PUBLIC_KEY')
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/VinithaAshokSingh/terraform-azure-vm.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh '''
                  rm -rf .terraform
                  terraform init -upgrade
                '''
            }
        }

        stage('Terraform Plan') {
            steps {
                sh '''
                  terraform plan -input=false
                '''
            }
        }

        stage('Terraform Apply') {
            steps {
                sh '''
                  terraform apply -auto-approve -input=false
                '''
            }
        }
    }
}

