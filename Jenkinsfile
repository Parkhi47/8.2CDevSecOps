pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clone your repository
                git branch: 'main', url: 'https://github.com/your_github_username/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Windows-friendly command
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests but continue even if some fail
                bat 'npm test || exit 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                // Run coverage script; continue on errors
                bat 'npm run coverage || exit 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                // Run security scan
                bat 'npm audit || exit 0'
            }
        }
    }
}
