def alljob = JOB_NAME.tokenize('/') as String[]
def proj_name = alljob[1]
pipeline {
  agent any
  stages {
    stage('') {
      steps {
        sh 'echo ${proj_name}'
      }
    }
  }
}
