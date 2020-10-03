pipeline {
    agent {
        label 'master'
    }
    environment {
        APP_NAME="Clarusway-App"
        REPO_VERSION="App-${BUILD_NUMBER}"
        
        
    }
    stages {
        stage('creating ECR Repo') {
            steps {
                echo 'creating ECR Repo'
                echo "Build number is:: ${BUILD_NUMBER}"
                echo "Workspace path is ::: ${WORKSPACE}"
                sh 'echo trying like in linux::: $JENKINS_URL'
            }
        }
        stage('building Docker image') {
            steps {
                echo 'building Docker image'
                echo "Application Name is:: ${APP_NAME}"
                echo "Repo version is ::: ${REPO_VERSION}"
                sh docker build --force-rm -t "${ECR_REGISTRY}/${APP_NAME}:latest" .  
                //sh 'docker build ..'
            }
        }
        stage('pushing Docker image to ECR Repo') {
            steps {
                echo 'pushing Docker image to ECR Repo'
                sh aws ecr get-login-password --region ${AWS::Region} | docker login --username AWS --password-stdin ${ECR_REGISTRY}
                // sh 'aws ecr get-login-password ... '
                sh docker push "${ECR_REGISTRY}/${APP_NAME}:latest" 
                // sh 'docker push ... '
            }
        }
        stage('creating infrastructure for the app') {
            steps {
                echo 'creating infrastructure for the app'
                
                
                "clarusway-jenkins-with-git-docker-ecr-cfn.yml" -L https://raw.githubusercontent.com/JeffU1/aws-workshop/master/204-jenkins-pipeline-for-phonebook-app-on-docker-swarm%20copy/clarusway-jenkins-with-git-docker-ecr-cfn.yml
                sh 'aws cloudformation create-stack --stack-name myteststack --region us-east-1 --template-body file://clarusway-jenkins-with-git-docker-ecr-cfn.yml --parameters ParameterKey=KeyPairName,ParameterValue=Hattusas'
                script {
                    int counter = 0 ;
                    while ( counter < 3 ) {
                        println('Counting... ' +counter);
                        sleep(2)
                        counter++;
                        //sh 'aws ec2 describe ...' get ip
                        //if (ip.length 7 ) ... break
                        //else sleep(10)
                    }
                }
            }
        }
        stage('test the Viz App') {
            steps {
                echo 'test the Viz App'
                script {
                    int counter = 0 ;
                    while ( counter < 3 ) {
                        println('Counting... ' +counter);
                        sleep(2)
                        counter++;
                        //try catch block with groovy/java
                        //sh 'curl ip:8080 ...' break
                        //failure ... sleep(5)
                    }
                }
            }
        }
        stage('deploying the application') {
            steps {
                echo 'deploying the application'
                sh 'mssh .... git clone'
                sh 'mssh .... docker stack deploy'
            }
        }
        stage('test phonebook the application') {
            steps {
                echo 'test phonebook the application'
                script {
                    int counter = 0 ;
                    while ( counter < 3 ) {
                        println('Counting... ' +counter);
                        sleep(2)
                        counter++;
                        //try catch block with groovy/java
                        //sh 'curl ip:8080 ...' break
                        //failure ... sleep(5)
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Goodbye ALL... Please come back soon'
        }
        failure {
            echo 'Sorry but you messed up...'
        }
        success { 
            echo 'You are the man/woman...'
        }
    }
}


// benim deneme - create basarili ama user doesnt have permission

pipeline {
    agent {
        label 'master'
    }
    stages {
        stage ('create ECR repo') {
            steps { 
                echo 'creating ECR repo'
            }
        }
        
        stage ('build docker image') {
            steps {
                echo 'build docker image'
            }
        }
        
        stage ('push docker image to ECR'){
            steps {
                echo 'push image to ECR'
            }
        }
        stage('creating infrastructure for the app') {
            steps {
                echo 'creating infrastructure for the app'
            }
        }
        
        stage('git clone') {
            steps {
                 git 'https://github.com/JeffU1/project204'
            }
        }
        
        stage ('continue creating') {
                steps {
                sh 'aws cloudformation create-stack --stack-name myteststack --region us-east-1 --template-body file://clarusway-jenkins-with-git-docker-ecr-cfn.yml --parameters ParameterKey=KeyPairName,ParameterValue=Hattusas --capabilities CAPABILITY_NAMED_IAM'
                }
            }
        
        stage ('deploy application') {
            steps {
                echo 'deploy application'
                }
        }
        
        stage ('check AWS Cli') {
            steps {
                sh 'aws --version'
            }
        }
    }
}

