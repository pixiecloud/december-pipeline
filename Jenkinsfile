pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="368085106192"
        AWS_DEFAULT_REGION="us-east-1"
        IMAGE_REPO_NAME="soso-repository"
        IMAGE_TAG="latest"
        REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
    }
           
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/sosotechnologies/december-pipeline.git']]])
            }
        }
  
 // Building Docker images
    stages {
    stage('Build') {
      steps {
        sh 'docker build -t sosotech/dp-alpine:latest .'
      }
    }
   
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push sosotech/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
    }
}
    
    
