pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('karim-dockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'docker build -t myapp/flask:latest .'
            }
        }
        stage('login to dockerhub') {
            steps{
                    bat "echo docker login -u stephanschweitzer -p Kierkegaard2014!"
            }
        }
        stage('push image') {
            steps{
                sh 'docker push myapp/flask:latest'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
