pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Simulate a build step
                sh 'echo "Build logs..." > build.log'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Simulate test step
                sh 'echo "Test logs..." > test.log'
            }
            post {
                always {
                    emailext(
                        subject: "Pipeline Test Stage - ${currentBuild.currentResult}",
                        body: "Hello,\n\nThe Test stage has completed with status: ${currentBuild.currentResult}.\nPlease find the attached test logs.",
                        to: "parkhi5200@example.com",
                        attachLog: true,
                        attachmentsPattern: 'test.log',
                        mimeType: 'text/plain'
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                // Simulate security scan step
                sh 'echo "Security scan logs..." > scan.log'
            }
            post {
                always {
                    emailext(
                        subject: "Pipeline Security Scan Stage - ${currentBuild.currentResult}",
                        body: "Hello,\n\nThe Security Scan stage has completed with status: ${currentBuild.currentResult}.\nPlease find the attached security scan logs.",
                        to: "developer@example.com",
                        attachLog: true,
                        attachmentsPattern: 'scan.log',
                        mimeType: 'text/plain'
                    )
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed with status: ${currentBuild.currentResult}"
        }
    }
}
