pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('karim-dockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                bat 'docker build -t stephanschweitzer/myapp-flask:latest .'
            }
        }
        stage('login to dockerhub') {
            steps{
                    bat "echo docker login -u stephanschweitzer -p Kierkegaard2014!"
            }
        }
        stage('push image') {
            steps{
                bat 'docker push stephanschweitzer/myapp-flask:latest'
            }
        }
}
post {
        always {
            bat 'docker logout'
        }
    }
}
