pipeline {
    agent { label 'agent1' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/afsha-munshi98/node-todo-cicd.git', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t afshamunshi/node-todo-test:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubPassword', usernameVariable: 'dockerhubUser')]) {
        	     sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                 sh 'docker push afshamunshi/node-todo-test:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
