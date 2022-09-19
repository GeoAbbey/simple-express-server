pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/GeoAbbey/simple-express-server', branch: 'main')
      }
    }

    stage('Log') {
      steps {
        sh 'ls -la'
      }
    }

    stage('Build Docker') {
      steps {
        sh 'docker build -f simple-express-server/Dockerfile .'
      }
    }

  }
}