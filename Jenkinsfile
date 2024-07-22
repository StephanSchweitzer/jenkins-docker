pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('karim-dockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                bat 'sudo docker build -t myapp/flask:latest .'
            }
        }
        stage('login to dockerhub') {
            steps{
                    bat "echo docker login -u stephanschweitzer -p Kierkegaard2014!"
            }
        }
        stage('push image') {
            steps{
                bat 'sudo docker push myapp/flask:latest'
            }
        }
}
post {
        always {
            bat 'docker logout'
        }
    }
}
