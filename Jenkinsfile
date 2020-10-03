pipeline {
    agent {
        label 'master'
    }
    environment {
        ECR_REGISTRY = "830561544145.dkr.ecr.us-east-1.amazonaws.com"
        APP_REPO_NAME = "cem-repo/phonebook-app"
        AWS_REGION = "us-east-1"
    }
    stages {
        stage('Create ECR Repo') {
            steps {
            echo 'creating ECR Repo'
            sh """ 
            aws ecr create-repository \ 
                --repository-name ${APP_REPO_NAME} \
                --image-scanning-configuration scanOnPush=false \
                --image-tag-mutability MUTABLE \
                --region ${AWS_REGION}
            """
            }
        }        
        stage('Building App Docker Images') {
            steps {
               echo 'Building app Docker images'     
            }
        }
        stage('Push App Docker Images to ECR Repo') {
            steps {
               echo 'Pushing  Docker images to ECR'     
            }
        }
        stage('Create Infrastructure for the App') {
            steps {
               echo 'creating Docker Swarm'     
            }
        }
        
        stage('Test Infrastructure') {
            steps {
               echo 'Testing if Docker Swarm is ready or not'     
            }
        }

        stage('Deploy the App on Swarm') {
            steps {
               echo 'Deploying the App'     
            }
        }
        stage('Test the App') {
            steps {
               echo 'Check if the App is ready or not'     
            }
        }
    }
    post {
        always {
            echo 'Deleting all local images'
        }
        failure {
            echo 'Deleting the image repository on ECR due to failure'
            echo 'Deleting the CloudFormation stack due to failure'
        }
    }
}

