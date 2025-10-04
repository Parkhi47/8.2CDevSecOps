pipeline {
    agent any

    environment {
        NODE_ENV = 'development'
        EMAIL_RECIPIENT = 'parkhi5200@gmail.com'  // Replace with your email
        CACHE_DIR = "${WORKSPACE}\\.cache_node_modules"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/Parkhi47/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Optional caching of node_modules
                    if (fileExists("${CACHE_DIR}\\package-lock.json")) {
                        echo "Restoring cached node_modules..."
                        bat "xcopy /E /I /Y ${CACHE_DIR}\\node_modules .\\node_modules"
                    }

                    // Install npm dependencies
                    bat 'npm install'

                    // Save node_modules to cache
                    bat "if not exist ${CACHE_DIR} mkdir ${CACHE_DIR}"
                    bat "xcopy /E /I /Y node_modules ${CACHE_DIR}\\node_modules"
                    bat "copy package-lock.json ${CACHE_DIR}\\package-lock.json"
                }
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0' // continue even if tests fail
            }
            post {
                always {
                    emailext(
                        subject: "Jenkins: Run Tests Stage - ${currentBuild.currentResult}",
                        body: "The 'Run Tests' stage finished with status: ${currentBuild.currentResult}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0' // continue even if audit finds vulnerabilities
            }
            post {
                always {
                    emailext(
                        subject: "Jenkins: NPM Audit Stage - ${currentBuild.currentResult}",
                        body: "The 'NPM Audit' stage finished with status: ${currentBuild.currentResult}",
                        attachLog: true,
                        to: "${EMAIL_RECIPIENT}"
                    )
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
