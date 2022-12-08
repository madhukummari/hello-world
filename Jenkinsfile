pipeline {
  agent any
  stages {

    stage('Stage-0 : Static Code Analysis Using SonarQube') { 
            steps {
                sh 'mvn clean verify sonar:sonar -DskipTests'
            }
        }
    stage ('stage-1 Build') {
      steps {
        sh 'mvn clean package install'
      }
    }
    stage ('stage-3 Deploy') {
      steps {
        
        script {
          deploy adapters: [tomcat9(credentialsId: 'bcb62da9-e087-4bc0-b4b7-2ae9cab6495b', path: '', url: 'http://34.228.40.56:8080')], contextPath: '/pipeline', onFailure: false, war: '**/*.war' 
        }
      }
    }
  }
}