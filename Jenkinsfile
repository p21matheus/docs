def jobnameparts = JOB_NAME.tokenize('/') as String[]
def jobconsolename = jobnameparts[0]
pipeline {
  agent any
  stages {
    stage('') {
      steps {
        sh 'echo ${jobconsolename}'
      }
    }
  }
}
