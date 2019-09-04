pipeline {
  def build = Thread.currentThread().toString()
  def regexp= ".+?/job/([^/]+)/.*"
  def match = build  =~ regexp
  def jobName = match[0][1]
  
  agent any
  stages {
    stage('saa') {
      steps {
        echo jobName
        echo '${env.JOB_NAME}'
      }
    }
  }
}
