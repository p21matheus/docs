pipeline {
  agent any
   stages {
    stage('Deploy') {
          steps {
            script {
                 if (env.JOB_NAME == 'doc/teste') {
                    if (env.BRANCH_NAME == 'teste') {
                      sh 'browsers=$(echo "${JOB_NAME}" | awk \'{print substr($1,0,3)}\') && echo ${browsers}'
                    } else {
                      echo 'things and stuff'
                    }
                 }
            }
          }
        }
  }
}
