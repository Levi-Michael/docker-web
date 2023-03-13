pipeline {
    agent {
        label 'master'
    }
    environment {
        AWS_ACCOUNT_ID="aws-credentials"
        AWS_DEFAULT_REGION="eu-central-1"
        IMAGE_REPO_NAME="my-nginx"
        IMAGE_TAG="v1"
        REPOSITORY_URI = "064055967665.dkr.ecr.eu-central-1.amazonaws.com/terraformecr"
    }
    stages {
        stage('Git-Checkout') {
            agent {
                label 'master'
            }
            steps {
                echo "Checking out from Git Repo";
		        git branch: 'main', url: 'https://github.com/Levi-Michael/Web-CI-CD.git';
            }
        }
        stage('Build') {
        agent {
            label 'master'
        }
        steps {
                script{
                        sh "docker build -t ${IMAGE_REPO_NAME}:${IMAGE_TAG} ."
                        sh "docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} 064055967665.dkr.ecr.eu-central-1.amazonaws.com/terraformecr:${IMAGE_REPO_NAME}"
                    }
                    
                }
            }
        }
        stage('Push') {
        agent {
            label 'master'
        }
        steps {
                script{
                        docker.withRegistry("https://064055967665.dkr.ecr.eu-central-1.amazonaws.com/terraformecr", "ecr:eu-central-1:aws-credentials") {
                        sh "sudo docker push 064055967665.dkr.ecr.eu-central-1.amazonaws.com/terraformecr:${IMAGE_REPO_NAME}"
                    }
                    
                }
            }
        }

    }
