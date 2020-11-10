pipeline {
  agent any

  triggers {
      pollSCM('* * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'docker build -t pokedex-go .'
      }
    }
    stage('Test') {
      steps {
        sh 'docker run --rm pokedex-go:latest npm test'
      }
    }
    stage('Deploy') {
      steps {
        sh 'docker rm -f mypokedex || true'
        sh 'docker run -d --rm -p 5555:5555 --name mypokedex pokedex-go:latest'
      }
    }
  }
  
  post {
      always {
          cleanWs()
      }
  }
}