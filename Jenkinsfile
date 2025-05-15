pipeline {
  agent any

  environment {
    //NODE_HOME = '/usr/local/bin'  // Adjust path as per your Jenkins node
    //PATH = "${env.NODE_HOME}:${env.PATH}"
    NODE_HOME = "${env.HOME}/.nvm/versions/node/v22.15.0/bin"
    PATH = "${env.NODE_HOME}:${env.PATH}"

  }

  tools {
    nodejs 'NodeJS_22'  // Define this in Jenkins global tools
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/anithaganesan1/jenkins-angular-webhook.git'
      }
    }


    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Build') {
      steps {
        //sh 'ng build --configuration=production'
          sh 'ng build'

      }
    }

    stage('Archive Build Output') {
      steps {
        archiveArtifacts artifacts: 'dist/**/*.*', fingerprint: true
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
