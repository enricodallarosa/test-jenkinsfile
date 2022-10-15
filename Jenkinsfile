pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        node(label: 'agent1') {
          isUnix()
        }

      }
    }

  }
}