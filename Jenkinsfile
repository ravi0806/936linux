pipeline {

    agent any

    environment {

        AWS_REGION = 'ap-south-1'

        IMAGE_NAME = 'mobile-store'

        AWS_ACCOUNT_ID = '391824190386'

        ECR_REPO = "391824190386.dkr.ecr.${ap-south-1}.amazonaws.com/mobile-store"
    }

    stages {

        stage('Clone Code') {

            steps {

                echo 'GitHub Code Pulled Successfully'

            }
        }

        stage('Build Docker Image') {

            steps {

                sh 'docker build -t mobile-store .'

            }
        }

        stage('Login To ECR') {

            steps {

                sh '''
                aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 391824190386.dkr.ecr.ap-south-1.amazonaws.com
                '''

            }
        }

        stage('Tag Docker Image') {

            steps {

                sh 'docker tag mobile-store:latest mobile-store:latest'

            }
        }

        stage('Push Image To ECR') {

            steps {

                sh 'docker push mobile-store:latest'

            }
        }

        stage('Deploy To EKS') {

            steps {

                sh 'kubectl apply -f k8s/'

            }
        }

    }

}