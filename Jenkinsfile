pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull code from your GitHub repo
                git branch: 'main', url: 'https://github.com/Parkhi47/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Linux/macOS
                // sh 'npm install'

                // Windows (Jenkins running on Windows agent)
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Linux/macOS
                // sh 'npm test || true'

                // Windows
                bat 'npm test || exit /b 0'  // Continue pipeline even if tests fail
            }
        }

        stage('Generate Coverage Report') {
            steps {
                // Linux/macOS
                // sh 'npm run coverage || true'

                // Windows
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                // Linux/macOS
                // sh 'npm audit || true'

                // Windows
                bat 'npm audit || exit /b 0'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}
