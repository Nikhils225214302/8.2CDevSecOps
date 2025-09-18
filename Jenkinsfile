pipeline {

   agent { label 'built-in' }
  environment {
    PATH = "/opt/homebrew/bin:/opt/homebrew/sbin:/usr/bin:/bin"
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Nikhils225214302/8.2CDevSecOps.git'
      }
    }

    stage('Env Check') {TE
      steps {
        sh '''
          echo "System info:"
          uname -a
          echo "PATH is: $PATH"
          which node || echo "node not found"
          which npm || echo "npm not found"
          node -v || echo "node version not found"
          npm -v || echo "npm version not found"
        '''
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test || true'   // continue even if tests fail
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true' // show CVEs in console output
      }
    }
  }
}
