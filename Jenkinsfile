pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/JayCorp97/8.1CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
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
