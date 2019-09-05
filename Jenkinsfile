pipeline {
  agent any
  stages {
    stage('') {
      steps {
        script {
          def browsers = $( echo 'cra/master' |awk '{print substr($1,0,4)}')
            echo "Testing the ${browsers} browser"
        }
      }
    }
  }
}
