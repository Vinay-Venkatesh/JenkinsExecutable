pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'echo "Hello World"'
        sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
      }
    }
  stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }

    steps {
        withAWS(region: 'us-east-1', credentials: 's3') {
          sh 'echo "Uploading content with AWS creds"'
          s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', bucket: 'jenkins-html-file')
        }
      }
    }
  }
