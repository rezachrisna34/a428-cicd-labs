node {
    def appDir = 'react-app'
    
    stage('Checkout') {
        checkout scm
    }

    // Tahapan di dalam folder aplikasi
    dir(appDir) {
        stage('Install Dependencies') {
            sh 'npm install'
        }
        stage('Build') {
            sh 'export NODE_OPTIONS=--openssl-legacy-provider && npm run build'
        }
        stage('Test') {
            sh 'export NODE_OPTIONS=--openssl-legacy-provider && npm test -- --watchAll=false'
        }
    }

    // --- MANUAL APPROVAL DI SINI (Di luar dir appDir) ---
    stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap Deploy?'
    }

    // --- DEPLOY DI SINI ---
    stage('Deploy') {
        dir(appDir) {
            sh 'export NODE_OPTIONS=--openssl-legacy-provider && (npm start &)'
            echo 'Aplikasi berhasil di-deploy. Menunggu selama 1 menit...'
            sh 'sleep 60'
            sh 'pkill -f "react-scripts start" || true'
        }
    }
}
