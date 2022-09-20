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
        sh 'docker build -f Dockerfile . -t geoabbey/simple-express-server:latest'
      }
    }

    stage('Log into DockerHub') {
      environment {
        DOCKERHUB_USER = 'geoabbey'
        DOCKERHUB_PASSWORD = 'lollipop199'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

    stage('Push to DockerHub') {
      steps {
        sh 'docker push geoabbey/simple-express-server:latest'
      }
    }

    stage('Remove the running container') {
      steps {
        sh '''sudo kill -9 $(sudo lsof -t -i:4000)
docker rm --force geoabbey/simple-express-server:latest'''
      }
    }

    stage('Run Docker Image') {
      steps {
        sh 'docker run -p 4000:4000 -d geoabbey/simple-express-server:latest'
      }
    }

  }
  triggers {
    githubPush()
  }
}