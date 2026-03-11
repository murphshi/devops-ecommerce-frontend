pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Test') {
            steps {
                sh 'CI=true npm test -- --watchAll=false --passWithNoTests'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Security scan stage placeholder'
            }
        }

        stage('Container Build') {
            steps {
                sh 'docker build -t ecommerce-frontend:jenkins .'
            }
        }

        stage('Container Push') {
            steps {
                echo 'Container push stage placeholder'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy stage placeholder'
            }
        }
    }
}
