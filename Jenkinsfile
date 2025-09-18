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

    stage('Env Check') {
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
        sh 'npm test || true'   
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true' 
      }
    }
  }
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

    stage('Env Check') {
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
      steps { sh 'npm install' }
    }

    stage('Run Tests') {
      steps { sh 'npm test || true' }   
    }

    stage('Generate Coverage Report') {
      steps { sh 'npm run coverage || true' }
    }

    stage('NPM Audit (Security Scan)') {
      steps { sh 'npm audit || true' }  
    }

   
    stage('SonarCloud Analysis') {
      steps {
        withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
          sh '''
            set -e
            SCANNER_VER=6.2.1.4610
            SCANNER_ZIP=sonar-scanner-cli-${SCANNER_VER}-linux.zip
            curl -fsSLO https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/$SCANNER_ZIP
            unzip -qo $SCANNER_ZIP
            export PATH="$PWD/sonar-scanner-${SCANNER_VER}-linux/bin:$PATH"
            sonar-scanner
          '''
        }
      }
    }
  }
}

}
