pipeline {
  agent any

  tools {nodejs "nodejs"}

  environment {
    NODE_ENV = 'production'
  }

  stages {
    stage('Clean up') {
      steps {
        cleanWs()    
      }
    }

    stage('Download dependencies') {
      steps {
        sh 'npm i'
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }

    stage('Publish to VM') {
      steps {
        sshPublisher(publishers: [sshPublisherDesc(configName: 'taylorsvm lhci', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/ubuntu/workspace/app', remoteDirectorySDF: false, removePrefix: 'dist', sourceFiles: 'dist/*')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])      }
    }

  }
}
