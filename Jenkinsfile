pipeline {
  agent any
  stages {
    stage('') {
      steps {
        sh 'projectName = ${JOB_NAME} | awk '{print $3}'
        sh 'echo projectName'
      }
    }
  }
}
