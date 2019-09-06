pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        script {
          sh browsers=echo ${JOB_NAME} | awk '{print substr($1,0,4)}'
        }

      }
    }
  }
}