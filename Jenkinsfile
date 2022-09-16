pipeline {
  agent any

  tools {nodejs "nodejs"}

  environment {
    NODE_ENV = 'production'
  }

  stages {
    stage('Check for vulnerabilities') {
      steps {
        sh 'npm audit --parseable --production'
        sh 'npm outdated || exit 0'
      }
    }

    stage('Download dependencies') {
      steps {
        sh 'npm ci'
      }
    }
  }
}
