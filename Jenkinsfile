pipeline {
  agent {
    node {
      label 'windows'
    }

  }
  stages {
    stage('build') {
      steps {
        powershell(script: 'write-out "Hello!"', returnStdout: true)
      }
    }
  }
}