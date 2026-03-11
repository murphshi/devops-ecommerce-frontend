pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'CI=true npm test -- --watchAll=false --passWithNoTests'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Static analysis placeholder for frontend'
            }
        }

        stage('Container Build') {
            steps {
                script {
                    env.IMAGE_TAG = "build-${env.BUILD_NUMBER}"
                    sh "docker build -t ecommerce-frontend:${env.IMAGE_TAG} ."
                }
            }
        }

        stage('Container Push') {
            steps {
                echo "Container push placeholder for ecommerce-frontend:${env.IMAGE_TAG}"
            }
        }

        stage('Build Environment Validation') {
            when {
                expression {
                    return !(env.GIT_BRANCH?.contains('develop') ||
                             env.GIT_BRANCH?.contains('release/') ||
                             env.GIT_BRANCH?.contains('main'))
                }
            }
            steps {
                echo "Build pipeline executed for feature branch or pull request validation on ${env.GIT_BRANCH}"
            }
        }

        stage('Deploy to Dev') {
            when {
                expression {
                    return env.GIT_BRANCH?.contains('develop')
                }
            }
            steps {
                echo "Deploying frontend to dev environment from ${env.GIT_BRANCH}"
            }
        }

        stage('Deploy to Staging') {
            when {
                expression {
                    return env.GIT_BRANCH?.contains('release/')
                }
            }
            steps {
                echo "Deploying frontend to staging environment from ${env.GIT_BRANCH}"
            }
        }

        stage('Prod Approval') {
            when {
                expression {
                    return env.GIT_BRANCH?.contains('main')
                }
            }
            steps {
                input message: 'Approve deployment to production?', ok: 'Deploy'
            }
        }

        stage('Deploy to Prod') {
            when {
                expression {
                    return env.GIT_BRANCH?.contains('main')
                }
            }
            steps {
                echo "Deploying frontend to production environment from ${env.GIT_BRANCH}"
            }
        }
    }
}
