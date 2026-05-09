pipeline {
    agent any

    environment {
        IMAGE = 'rajbhimani18/self-healing-app:latest'
        DOCKER_CREDENTIALS = 'dockerhub-creds'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/RajBhimani-2003/k8s-self-healing-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    sudo docker build -t $IMAGE .
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: DOCKER_CREDENTIALS,
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                        echo $DOCKER_PASS | sudo docker login -u $DOCKER_USER --password-stdin
                        sudo docker push $IMAGE
                    '''
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    sudo kubectl apply -f deployment.yaml
                    sudo kubectl apply -f service.yaml
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    sudo kubectl rollout status deployment/self-healing-app
                    sudo kubectl get pods
                    sudo kubectl get svc
                '''
            }
        }
    }

    post {
        success {
            echo 'Self-Healing Kubernetes deployment completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check console output for details.'
        }
    }
}