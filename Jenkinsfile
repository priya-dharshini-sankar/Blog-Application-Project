pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                dir('backend') {
                    sh 'npm ci'
                }

                dir('frontend') {
                    sh 'npm ci'
                    sh 'npm run build'
                }
            }
        }

        stage('SonarQube Analysis') {
    steps {
        script {
            def scannerHome = tool 'SonarScanner'

            withSonarQubeEnv('SonarQube') {
                sh "${scannerHome}/bin/sonar-scanner " +
                   "-Dsonar.projectKey=Blog-Application " +
                   "-Dsonar.projectName='Blog Application'"
            }
        }
    }
}

        stage('Quality Gate') {
            steps {
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build -t blog-frontend:${BUILD_NUMBER} ./frontend
                    docker build -t blog-backend:${BUILD_NUMBER} ./backend
                '''
            }
        }

        stage('Trivy Scan') {
            steps {
                sh '''
                    trivy image blog-frontend:${BUILD_NUMBER}
                    trivy image blog-backend:${BUILD_NUMBER}
                '''
            }
        }
    }
}

        


