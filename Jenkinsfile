pipeline {
    agent any
    stages {
        stage("Clone Code"){
            steps {
                git url: "https://github.com/SyedWasifAbbas5/node-todo-app-cicd.git", branch: "main"
            }
        }
        
        stage("Build and Test"){
            steps{
                sh "docker build . -t node-todo-app:latest"
            }
        }
        
        stage("Push to Docker Hub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag node-todo-app ${env.dockerHubUser}/node-todo-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/node-todo-app:latest"
                }
            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
