pipeline {
    agent any

    tools {
        maven 'Maven-3.10'
    }

    stages {
        stage('1. Checkout') {
            steps {
                checkout scm
            }
        }

        stage('2. Build and Test') {
            steps {
                bat 'mvn clean test'
            }
        }

        stage('3. Package JAR') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }

        stage('4. Build Docker Image') {
            steps {
                bat 'docker build -t campus-equipment-booking:set-f .'
            }
        }

        stage('5. Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f k8s-deployment.yaml --validate=false'
                bat 'kubectl rollout status deployment/booking-deployment'
            }
        }
    }
}
