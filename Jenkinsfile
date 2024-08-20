pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      steps {
        git(credentialsId: 'githubkey', url: 'https://github.com/Aswin-tech-07/capstone.git')
        echo 'Git Checkout Completed'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t aswin3498/capstone_production:latest .'
        echo 'docker build completed'
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        echo 'docker logged in'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push aswin3498/capstone_production:latest'
        echo 'docker image published'
      }
    }

  }
  post {
    always {
      sh 'docker logout'
      echo 'docker logged out'
    }

  }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
}