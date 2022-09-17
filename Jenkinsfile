pipeline {
  agent any

  tools {nodejs "nodejs"}

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
        sh 'npm i @lhci/cli'
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build-only'
      }
    }

    stage('Publish to VM') {
      steps {
        sshPublisher(publishers: [sshPublisherDesc(configName: 'taylorsvm lhci', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/workspace/app', remoteDirectorySDF: false, removePrefix: 'dist', sourceFiles: 'dist/')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])      }
    }

    stage('Lighthouse Test') {
      steps {
        sh 'lhci collect'
        sh 'lhci upload'
      }
    }
  }
}
