pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/Jimblessed/curriculum-app', branch: 'dev')
      }
    }

    stage('log') {
      parallel {
        stage('log') {
          steps {
            sh 'ls -la'
          }
        }

        stage('Front-End Unit Tests') {
          steps {
            sh 'cd curriculum-front npm run test:unit'
          }
        }

      }
    }

    stage('Build') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile .'
      }
    }

    stage('log into Dockerhub') {
      environment {
        DOCKERHUB_USER = 'jimblaze77@gmail.com'
        DOCKERHUB_PASSWORD = 'Cloud123$'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USER -p $DOCKERHUB_PASSWORD'
      }
    }

  }
}