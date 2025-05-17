pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'janithabomi@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/JayCorp97/8.1CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    bat 'echo Running simulated tests... || exit /b 0'
                }
            }
            post {
                always {
                    emailext(
                        subject: "Run Tests Stage: ${currentBuild.currentResult}",
                        body: "Run Tests stage completed with status: ${currentBuild.currentResult}",
                        to: "${env.EMAIL_RECIPIENT}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'echo Simulated coverage report... || exit /b 0'
            }
            post {
                always {
                    emailext(
                        subject: "Coverage Report Stage: ${currentBuild.currentResult}",
                        body: "Coverage generation stage completed with status: ${currentBuild.currentResult}",
                        to: "${env.EMAIL_RECIPIENT}",
                        attachLog: true
                    )
                }
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE') {
                    bat 'npm audit'
                }
            }
            post {
                always {
                    emailext(
                        subject: "Security Scan Stage: ${currentBuild.currentResult}",
                        body: "Security scan stage completed with status: ${currentBuild.currentResult}",
                        to: "${env.EMAIL_RECIPIENT}",
                        attachLog: true
                    )
                }
            }
        }
    }
}
