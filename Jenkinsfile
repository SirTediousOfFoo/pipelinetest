pipeline {
  agent any
  stages {
    stage('build image') {
      steps {
        git(url: 'https://github.com/SirTediousOfFoo/pipelinetest.git', branch: 'master', changelog: true)
        sh 'docker build .'
      }
    }

  }
}