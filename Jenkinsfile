pipeline {
  agent any

  tools {
    nodejs 'NodeJS_22'  // Make sure this is configured in Global Tool Configuration
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/anithaganesan1/jenkins-angular-webhook.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm ci'
      }
    }

    stage('Run Build') {
      steps {
        sh 'ng build'
      }
    }

    stage('Archive Build Output') {
      steps {
        archiveArtifacts artifacts: 'dist/**', fingerprint: true
      }
    }
  }

  post {
    success {
      mail to: 'aniganesan86@gmail.com',
           subject: "SUCCESS: Angular Build #${env.BUILD_NUMBER}",
           body: "The Angular project built successfully. Check Jenkins artifacts."
    }
    failure {
      mail to: 'aniganesan86@gmail.com',
           subject: "FAILURE: Angular Build #${env.BUILD_NUMBER}",
           body: "The Angular build failed. Please review Jenkins logs."
    }
  }
}
