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

        stage('Trivy Scan') {
            steps {
                sh '''
                    trivy image 196253396965.dkr.ecr.ap-south-1.amazonaws.com/blog-frontend:tag1

                    trivy image 196253396965.dkr.ecr.ap-south-1.amazonaws.com/blog-backend:tag1
                '''
            }
        }
    }
}

        


