pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        sh '''browsers=$(echo "CRA/TESE" | awk \'{print substr($1,0,4)}\') && echo ${browsers}
'''
      }
    }
  }
}