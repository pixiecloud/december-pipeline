pipeline {
    agent any
    environment {
       DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    }
           
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/sosotechnologies/december-pipeline.git']]])
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
    
    
