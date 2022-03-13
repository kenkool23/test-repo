pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/kenkool23/test-repo.git'
            }
        }
        
        stage('Build and Tag Image') {
            steps {
                script {
                app = docker.build("855171129788.dkr.ecr.us-east-1.amazonaws.com/testrepo:${BUILD_NUMBER}")
                }
            }
        }
        
        stage('Push image to ECR') {
            steps {
                script {
                docker.withRegistry("https://855171129788.dkr.ecr.us-east-1.amazonaws.com/testrepo", "ecr:us-east-1:ecr-registry") {
                app.push()
                app.push('latest')
                }
                 }
            }
        }
    }
}
