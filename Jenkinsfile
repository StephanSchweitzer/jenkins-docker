pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('karim-dockerhub')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/StephanSchweitzer/jenkins-docker']]
                ])
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def buildCommand = 'docker build -t stephanschweitzer/myapp-flask:latest .'
                    if (isUnix()) {
                        sh buildCommand
                    } else {
                        bat buildCommand
                    }
                }
            }
        }
        stage('Login to DockerHub') {
            steps {
                script {
                    def loginCommand = 'echo docker login -u stephanschweitzer -p Kierkegaard2014!'
                    if (isUnix()) {
                        sh loginCommand
                    } else {
                        bat 'echo docker login -u stephanschweitzer -p Kierkegaard2014!'
                    }
                }
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    def pushCommand = 'docker push stephanschweitzer/myapp-flask:latest'
                    if (isUnix()) {
                        sh pushCommand
                    } else {
                        bat pushCommand
                    }
                }
            }
        }
    }
    post {
        always {
            script {
                def cleanupCommand = 'docker rmi stephanschweitzer/myapp-flask:latest'
                if (isUnix()) {
                    sh cleanupCommand
                } else {
                    bat cleanupCommand
                }
            }
        }
    }
}
