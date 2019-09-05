pipeline {
  agent any
  stages {
    stage('') {
      steps {
        sh 'val=$( echo "cra/master" $len|awk '{print substr($1,0,4)}')'
        sh 'echo $val'
      }
    }
  }
}
