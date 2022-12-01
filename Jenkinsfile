pipeline {
  agent any
  stages {
    stage ('Build') {
      steps {
        sh 'mvn clean package install'
      }
    }
    stage ('Deploy') {
      steps {
        script {
          deploy adapters: [tomcat9(credentialsId: 'bcb62da9-e087-4bc0-b4b7-2ae9cab6495b', path: '', url: 'http://54.89.254.123:8080')], contextPath: '/pipeline', onFailure: false, war: '**/*.war' 
        }
      }
    }
  }
}