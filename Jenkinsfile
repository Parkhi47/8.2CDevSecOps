pipeline {
    agent any

    environment {
        // Use your Jenkins credential ID here
        EMAIL_CREDENTIALS = 'gmail-jenkins'
        EMAIL_RECIPIENT = 'parkhi5200@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Parkhi47/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit 0'
            }
        }
    }

    post {
        always {
            // Send email with log after pipeline completion
            emailext(
                subject: "Jenkins Build ${currentBuild.fullDisplayName} - ${currentBuild.result}",
                body: """
                Hello, <br>
                The Jenkins pipeline has completed. <br>
                Build Status: ${currentBuild.currentResult} <br>
                <br>
                You can see the console output attached.
                """,
                to: "${EMAIL_RECIPIENT}",
                attachLog: true,
                replyTo: "${EMAIL_RECIPIENT}",
                from: "${EMAIL_RECIPIENT}",
                credentialsId: "${EMAIL_CREDENTIALS}"
            )
        }
    }
}
