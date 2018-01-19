pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        dockerfile {
          filename 'Dockerfile'
          additionalBuildArgs '--build-arg version=1.1 -t epas:test'
        }
      }
      steps {
        sh 'python -c "import sys;print(sys.executable, sys.version)"'
        sh 'ls -al'
        sh 'pwd'
      }
      post {
        always {
          sh 'printenv'
        }
      }
    }
    stage('Test') {
        agent any
        steps{
            sh 'docker run --rm -d  --name $BUILD_TAG -p 80:80 epas:test'
            sh 'curl -v `docker inspect --format="{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" $BUILD_TAG`'
        }
        post {
            always {
                sh 'docker stop $BUILD_TAG'
            }
        }
    }
  }
}
