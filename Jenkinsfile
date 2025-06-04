pipeline {
  agent any

  environment {
    IMAGE_NAME = "shoheb2562/my-docker-app"
  }

  stages {
    stage('Clone') {
      steps {
        git 'https://github.com/Shoaibulhaq/my-docker-app.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE_NAME .'
      }
    }

    stage('Login to Docker Hub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
        }
      }
    }

    stage('Push Image') {
      steps {
        sh 'docker push $IMAGE_NAME'
      }
    }
  }

  post {
    always {
      cleanWs()
    }
  }
}
