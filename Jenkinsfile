pipeline {
  agent any
  stages {
    stage('Allocate WS and fill with data from Git') {
      steps {
        git(url: 'https://github.com/bliekp/BrouwHulp.git', branch: 'development', changelog: true, poll: true)
        sh '''pwd . && echo **** &&
ls -altrh . && echo **** &&

ls -al /var/services/homes/pim/Docker/pascal_files'''
      }
    }
    stage('Build') {
      steps {
        sh 'docker exec pascalContainer bash -c "cd /var/services/homes/pim/Docker/pascal_files && pwd && ls -altrh && fpc -va hello.pas"'
      }
    }
    stage('error') {
      steps {
        archiveArtifacts(allowEmptyArchive: true, caseSensitive: true, onlyIfSuccessful: true, artifacts: 'hello')
      }
    }
  }
}