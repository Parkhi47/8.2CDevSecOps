pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Tool: Git (version control)
                git branch: 'main', url: 'https://github.com/Parkhi47/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Tool: npm (Node.js package manager)
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Tool: npm test (Node.js testing framework, e.g., Mocha, Jest)
                bat 'npm test || exit 0'
            }
            post {
                always {
                    // Email notification after test stage
                    emailext(
                        subject: "Jenkins Test Stage - ${currentBuild.currentResult}",
                        body: "Hello,\n\nThe Test stage has completed. Check the attached logs for details.",
                        to: "parkhi5200@gmail.com",
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                // Tool: nyc/Istanbul (code coverage reporting for Node.js)
                bat 'npm run coverage || exit 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                // Tool: npm audit (dependency vulnerability scanner)
                bat 'npm audit || exit 0'
            }
            post {
                always {
                    // Email notification after security scan stage
                    emailext(
                        subject: "Jenkins Security Scan - ${currentBuild.currentResult}",
                        body: "Hello,\n\nThe NPM Audit stage has completed. Check the attached logs for details.",
                        to: "parkhi5200@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
    }
}
