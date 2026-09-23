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

        stage('ECR Push') {
            steps {
                sh '''
                    aws ecr get-login-password --region ap-south-1 | \
                    docker login --username AWS --password-stdin 196253396965.dkr.ecr.ap-south-1.amazonaws.com

                    docker tag blog-frontend:${BUILD_NUMBER} 196253396965.dkr.ecr.ap-south-1.amazonaws.com/blog-frontend:${BUILD_NUMBER}
                    docker tag blog-backend:${BUILD_NUMBER} 196253396965.dkr.ecr.ap-south-1.amazonaws.com/blog-backend:${BUILD_NUMBER}

                    docker push 196253396965.dkr.ecr.ap-south-1.amazonaws.com/blog-frontend:${BUILD_NUMBER}
                    docker push 196253396965.dkr.ecr.ap-south-1.amazonaws.com/blog-backend:${BUILD_NUMBER}
                '''
            }
        }

        stage('EKS Deployment') {
            steps {
                sh '''
                    aws eks update-kubeconfig \
                    --region ap-south-1 \
                    --name project-4-cluster

                    kubectl set image deployment/blog-frontend \
                    frontend=196253396965.dkr.ecr.ap-south-1.amazonaws.com/blog-frontend:${BUILD_NUMBER}

                    kubectl set image deployment/blog-backend \
                    backend=196253396965.dkr.ecr.ap-south-1.amazonaws.com/blog-backend:${BUILD_NUMBER}

                    kubectl rollout status deployment/blog-frontend
                    kubectl rollout status deployment/blog-backend
                '''
            }
        }

        stage('Deployment Validation') {
            steps {
                sh '''
                    kubectl get deployments
                    kubectl get pods
                    kubectl get services
                '''
            }
        }
    }
}

        

        






