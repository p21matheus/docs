pipeline {
  agent any
  def alljob = JOB_NAME.tokenize('/') as String[]
  def proj_name = alljob[1] //to capture a simple pipeline project name inside a manually created folder

  stages {
    stage('') {
      steps {
        sh 'echo proj_name'
      }
    }
  }
}
