pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        sh 'browsers=$(echo "${JOB_NAME}" | awk \'{print substr($1,0,3)}\') && echo ${browsers}'
      }
    }
  }
}