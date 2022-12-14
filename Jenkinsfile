pipeline {
  agent any
  stages {
    stage('build image') {
      steps {
        git(url: 'https://github.com/SirTediousOfFoo/pipelinetest.git', branch: 'master', changelog: true)
        sh 'TIME=$(date +%s)'
        sh 'docker build . -t company/superapp:$BUILD -t company/superapp:latest'
      }
    }

    stage('Test') {
      steps {
        sh 'docker run -p 8081:81 -p 8082:82 -p 8083:83 -d superapp:latest '
        echo 'App1 availability'
        sh '''
curl -f --show-error 127.0.0.1:8081/index.html'''
        echo 'App2 availability'
        sh 'curl -f --show-error 127.0.0.1:8081'
        echo 'App3 availability'
        sh 'curl -f --show-error 127.0.0.1:8083'
        sh '''curl -f --show-error 127.0.0.1:8082
'''
        sh 'docker kill $(docker ps -q)'
      }
    }

    stage('deploy image') {
      steps {
        echo '"echo $DOCKER_SECRET | docker login -u mysuperuser --password-stdin"'
        echo 'docker push company/superapp:$BUILD'
        echo 'kubectl apply -f deployment.yaml'
      }
    }

  }
  environment {
    BUILD = "${env.BUILD_ID}"
    DOCKER_SECRET = 'credentials(\'dockercreds\')'
  }
}