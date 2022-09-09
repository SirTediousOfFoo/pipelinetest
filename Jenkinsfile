pipeline {
  agent any
  stages {
    stage('build image') {
      steps {
        git(url: 'https://github.com/SirTediousOfFoo/pipelinetest.git', branch: 'master', changelog: true)
        sh 'docker build . -t superapp:$(date +%s)'
      }
    }

    stage('Test') {
      steps {
        sh 'docker run -p 8081:81 -p 8082:82 -p 8083:83 superapp:latest '
        echo 'App1 availability'
        sh '''
curl -f --show-error 127.0.0.1:8081/index.html'''
        echo 'App2 availability'
        sh 'curl -f --show-error 127.0.0.1:8081'
        echo 'App3 availability'
        sh 'curl -f --show-error 127.0.0.1:8083'
        sh '''curl -f --show-error 127.0.0.1:8082
'''
      }
    }

  }
}