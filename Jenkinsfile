pipeline {
    parameters {
        booleanParam(name: 'autoApprove', defaultValue: false, description: 'Automatically run apply after generating plan?')
    } 
    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

    agent any
    tools {
        terraform 'Terraform'
    }
    
    stages {
        stage('checkout') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/Yagmur1997/terraform-jenkins.git'
                }
            }
        }

        stage('Plan') {
            steps {
                sh 'terraform init'
                sh 'terraform plan -out tfplan'
                sh 'terraform show -no-color tfplan > tfplan.txt'
            }
        }

        stage('Apply') {
            steps {
                sh "terraform apply -input=false tfplan"
            }
        }
    }
  
  }