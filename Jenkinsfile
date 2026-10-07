pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Frontend Build') {
            steps {
                dir('OneSpace_Phase1') {
                    sh 'npm ci'
                    sh 'npm run build'
                }
            }
        }

        stage('Backend Build') {
            steps {
                dir('OneSpace_Phase1/server') {
                    sh 'npm ci'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -f Dockerfile.backend -t onespace-backend:${BUILD_NUMBER} .'
                sh 'docker tag onespace-backend:${BUILD_NUMBER} onespace-backend:latest'
            }
        }

        stage('Backend Health Test') {
            steps {
                sh '''
                    docker rm -f onespace-ci-test 2>/dev/null || true
                    docker run -d --name onespace-ci-test -p                    backend:${BUILD_NUMBER}

                    sleep 3

                    curl --fail http://127.0.0.1:5001/api/health

                    docker                    est
                '''
                                     st {
        always {
            sh 'docker rm            sh 'docker rdev/null || true'
        }
    }
}
