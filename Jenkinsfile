pipeline{
    agent any
    stages{
        stage("code"){
            steps{
                echo "Cloning the code"
                git url :"https://github.com/LondheShubham153/django-notes-app.git" , branch:"main"
            }
        }
        stage("Build"){
            steps{
                echo "Building the image"
                sh "docker build -t my-notes-app ."
            }
        }
        stage("push to docker Hub"){
            steps{
                echo "Pushing the image"
                withCredentials([usernamePassword(credentialsId: "dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploying"
                // sh "docker run -d -p 8000:8000 tanisha91/my-notes-app:latest"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
