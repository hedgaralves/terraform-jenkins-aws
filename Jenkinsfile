pipeline {
    agent any

    parameters {
        booleanParam(name: 'autoApprove', defaultValue: false, description: 'Automatically run apply after generating plan?')
        choice(name: 'action', choices: ['apply', 'destroy'], description: 'Select the action to perform')
    }

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_DEFAULT_REGION    = 'us-east-1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/hedgaralves/terraform-jenkins-aws.git', credentialsId: 'terraform-jenkins'
            }
        }

        stage('Terraform init') {
            steps {
                script {
                    try {
                        bat 'terraform init -input=false -no-color'
                    } catch (Exception e) {
                        echo "Terraform init failed: ${e}"
                        throw e
                    }
                }
            }
        }

        stage('Terraform Validate') {
            steps {
                bat 'terraform validate -no-color'
            }
        }

        stage('Terraform Lint') {
            steps {
                bat 'tflint --init'
                bat 'tflint'
            }
        }

        stage('Plan') {
            steps {
                bat 'terraform plan -out tfplan'
                bat 'terraform show -no-color tfplan > tfplan.txt'
            }
        }

        stage('Apply / Destroy') {
            steps {
                script {
                    if (params.action == 'apply') {
                        if (!params.autoApprove) {
                            def plan = readFile 'tfplan.txt'
                            input message: "Do you want to apply the plan?",
                            parameters: [text(name: 'Plan', description: 'Please review the plan', defaultValue: plan)]
                        }

                        bat 'terraform apply -input=false tfplan'
                    } else if (params.action == 'destroy') {
                        bat 'terraform destroy --auto-approve'
                    } else {
                        error "Invalid action selected. Please choose either 'apply' or 'destroy'."
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}