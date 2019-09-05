pipeline {
  agent any
  stages {
    stage('') {
      steps {
        script {
          def browsers=$(echo${JOB_NAME} |awk '{print substr($1,0,4)}')
          echo "Testing the ${browsers} browser"
        }
      }
    }
  }
}
