pipeline {
  agent any

  //tools {
    //nodejs 'NodeJS_22'
  //}
//cvv
  stages {
    //stage('Checkout')
      stage('Clone code')

    {
      steps {
        git url: 'https://github.com/anithaganesan1/jenkins-angular-webhook.git', branch: 'master'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm ci'
      }
    }

    stage('Verify CLI') {
      steps {
        sh 'ls -la ./node_modules/.bin'
        sh './node_modules/.bin/ng version || echo "ng CLI not found"'
      }
    }

    stage('Run Build') {
      steps {
        sh 'node -v'
        sh 'npm -v'
        sh './node_modules/.bin/ng build --configuration=production'
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
