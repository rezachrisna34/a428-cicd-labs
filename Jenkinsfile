node {
    def appDir = 'react-app'
    stage('Checkout') {
        checkout scm
    }
    dir(appDir) {
        stage('Install Dependencies') {
            sh 'npm install'
        }
        stage('Build') {
            // Gunakan legacy provider untuk Node v20
            sh 'export NODE_OPTIONS=--openssl-legacy-provider && npm run build'
        }
        stage('Test') {
            sh 'export NODE_OPTIONS=--openssl-legacy-provider && npm test -- --watchAll=false'
        }
    }
}
