pipeline {
    agent { label 'dev-agent' }
    stages{
        stage('Code'){
            steps {
                git url: 'https://github.com/surapkp/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Buid and Test'){
            steps {
                sh 'docker build . -t surapkp/node-todo-app-cicd:latest'
            }
        }
        stage('Docker Logging and Push image'){
            steps {
                echo "Login into Docker Hub and saved image"
                withCredentials([usernamePassword(credentialsId:"dockerhub", passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push surapkp/node-todo-app-cicd:latest"
                }
            }
        }
        stage('Deploy'){
            steps {
                sh 'docker-compose down  && docker-compose up -d'
            }
        }
    }
}
