pipeline {
    agent any

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
            post {
                always {
                    emailext (
                        subject: "Jenkins Pipeline: Run Tests - ${currentBuild.currentResult}",
                        body: """<p>Hello,</p>
                                 <p>The Run Tests stage has finished with status: ${currentBuild.currentResult}.</p>""",
                        to: 'parkhi5200@gmail.com',
                        attachLog: true
                    )
                }
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
            post {
                always {
                    emailext (
                        subject: "Jenkins Pipeline: Security Scan - ${currentBuild.currentResult}",
                        body: """<p>Hello,</p>
                                 <p>The Security Scan stage has finished with status: ${currentBuild.currentResult}.</p>""",
                        to: 'parkhi5200@gmail.com',
                        attachLog: true
                    )
                }
            }
        }
    }
}
