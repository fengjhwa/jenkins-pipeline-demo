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
      }
    }
  }
}
