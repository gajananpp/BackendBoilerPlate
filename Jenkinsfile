pipeline {
  agent any
  stages {
    stage('Export Version & Name') {
      steps {
        sh 'node /etc/detector'
      }
    }
    stage('Build Image') {
      steps {
        sh 'docker build -t $DOCKER_SERVER/$(cat NAME):$(cat VERSION) .'
      }
    }
    stage ('Docker push') {
      steps {
        docker.withRegistry('https://838855741485.dkr.ecr.ap-south-1.amazonaws.com', 'ecr:ap-south-1:demo-ecr-credentials') {
         docker.image('demo').push('latest')
        }
      }
    }
  }
  environment {
    KUBE_URL = credentials('KUBE_URL')
    KUBE_TOKEN = credentials('KUBE_TOKEN')
    DOCKER_SERVER = credentials('DOCKER_SERVER')
    DOCKER_USERNAME = credentials('DOCKER_USERNAME')
    DOCKER_PASSWORD = credentials('DOCKER_PASSWORD')
    SONARQUBE_SERVER = credentials('SONARQUBE_SERVER')
    SONARQUBE_USERNAME = credentials('SONARQUBE_USERNAME')
    SONARQUBE_PASSWORD = credentials('SONARQUBE_PASSWORD')
    SONAR_SCANNER_HOME = tool 'SonarQube Scanner'
  }
}
