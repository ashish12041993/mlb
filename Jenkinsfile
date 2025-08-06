pipeline {
    agent any

    environment {
        BRANCH = "${env.BRANCH_NAME}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "Running pipeline for branch: ${BRANCH}"
            }
        }

        stage('Build & Unit Test') {
            when {
                anyOf {
                    branch 'dev'
                    branch 'test'
                    branch 'main'
                }
            }
            steps {
                echo "Building and running unit tests on ${BRANCH}"
                // Example: sh 'npm install && npm run test'
            }
        }

        stage('Integration Test') {
            when {
                branch 'test'
            }
            steps {
                echo "Running integration tests on ${BRANCH}"
                // Example: sh './run-integration-tests.sh'
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying to staging from ${BRANCH}"
                // Example: sh './deploy-prod.sh'
            }
        }
    }

    post {
        success {
            echo "Build successful for ${BRANCH}"
        }
        failure {
            echo "Build failed for ${BRANCH}"
        }
    }
}
