pipeline {
  agent any
  tools {
    mvn
  }
  stages {
    stage ('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
  }
}
