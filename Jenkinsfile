pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Simulate a build step and save logs
                sh 'echo "Build logs..." > build.log'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Simulate test step and save logs
                sh 'echo "Test logs..." > test.log'
            }
            post {
                always {
                    script {
                        // Check if log exists before emailing
                        if (fileExists('test.log')) {
                            emailext(
                                subject: "Pipeline Test Stage - ${currentBuild.currentResult}",
                                body: """Hello,

The Test stage has completed with status: ${currentBuild.currentResult}.
Please find the attached test logs.""",
                                to: "parkhi5200@example.com",
                                attachLog: true,
                                attachmentsPattern: 'test.log',
                                mimeType: 'text/plain'
                            )
                        } else {
                            echo "Test log not found, skipping email attachment."
                        }
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                // Simulate security scan step and save logs
                sh 'echo "Security scan logs..." > scan.log'
            }
            post {
                always {
                    script {
                        if (fileExists('scan.log')) {
                            emailext(
                                subject: "Pipeline Security Scan Stage - ${currentBuild.currentResult}",
                                body: """Hello,

The Security Scan stage has completed with status: ${currentBuild.currentResult}.
Please find the attached security scan logs.""",
                                to: "developer@example.com",
                                attachLog: true,
                                attachmentsPattern: 'scan.log',
                                mimeType: 'text/plain'
                            )
                        } else {
                            echo "Security scan log not found, skipping email attachment."
                        }
                    }
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
