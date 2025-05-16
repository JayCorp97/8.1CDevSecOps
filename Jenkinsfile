pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/<your-username>/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Windows: use bat | Linux/Mac: use sh
                bat 'npm install'
            }
        }

        stage('Run Security Audit') {
            steps {
                bat 'echo Running npm audit for security check...'
                bat 'npm audit --audit-level=low'
            }
        }

        stage('Save Audit Report') {
            steps {
                bat 'npm audit --json > audit-report.json'
                archiveArtifacts artifacts: 'audit-report.json', fingerprint: true
            }
        }
    }
}
