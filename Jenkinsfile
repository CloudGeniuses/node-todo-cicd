pipeline {
    agent any
    
    stages {
        
        stage("code") {
            steps {
                git url: "https://github.com/CloudGeniuses/node-todo-cicd.git", branch: "master"
                echo 'bhaiyya code clone ho gaya'
            }
        }
        
        stage("build and test") {
            steps {
                bat "docker build -t cloudgeniuslab/node-todo-test ."
                echo 'code build bhi ho gaya'
            }
        }
        
        stage("scan image") {
            steps {
                echo 'image scanning ho gayi'
            }
        }
        
        stage("push") {
            steps {
                withCredentials([usernamePassword(credentialsId: "dockerhub-cred", passwordVariable: "dockerhubCredPass", usernameVariable: "dockerhubCredUser")]) {
                    bat "docker login -u ${dockerhubCredUser} -p ${dockerhubCredPass}"
                    bat "docker tag cloudgeniuslab/node-todo-test cloudgeniuslab/node-todo-test-job"
                    bat "docker push cloudgeniuslab/node-todo-test-job"
                    echo 'image push ho gaya'
                }
            }
        }
        
        stage("deploy") {
            steps {
                bat "docker-compose down && docker-compose up -d"
                echo 'deployment ho gayi'
            }
        }
    }
}
