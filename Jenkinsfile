pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        ECR_REPO = '966537025366.dkr.ecr.ap-south-1.amazonaws.com/my-app'
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/abhisheksajjan73-create/newproject.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t  javaking:latest'
            }
        }

        stage('Push to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin 966537025366.dkr.ecr.ap-south-1.amazonaws.com

                docker tag hello-java:latest $ECR_REPO:latest

                docker push $ECR_REPO:latest
                '''
            }
        }
    }
}
