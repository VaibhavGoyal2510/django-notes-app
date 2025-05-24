@Library("Shared") _
pipeline {
    agent {label "lovely"}
    
    stages{
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Code"){
            steps{
                // echo "This is cloning the code"
                // git url: "https://github.com/VaibhavGoyal2510/django-notes-app.git", branch:"main"
                // echo "Code cloning successful"
                script{
                    clone("https://github.com/VaibhavGoyal2510/django-notes-app.git","main")
                }
            }
        }
        //  stage("Install Docker"){
        //      steps{
        //          sh "sudo apt-get -y install docker.io "
        //          sh "sudo usermod -aG docker $USER"
        //          sh "sudo newgrp docker"
        //      }
        //  }
        stage("Build"){
            steps{
                // echo "This is building my friend"
                // sh "whoami"
                // sh "sudo docker build -t notes-app:latest ."
                script{
                    docker_build("notes-app","latest","killerbhaivg")
                }
            }
        }
        stage("Push To docker Hub"){
            steps{
                echo "This is pushing img to DOcker my friend"
                // withCredentials([usernamePassword('credentialsId':"docker-hub-cred",
                // passwordVariable:"dockerHubPass",
                // usernameVariable:"dockerHubUser")])
                // {
                // sh "sudo docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                // sh "sudo docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                // sh "sudo docker push ${env.dockerHubUser}/notes-app:latest"
                // }
                script{
                    docker_push("notes-app","latest","killerbhaivg")
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "This is deploying my friend"
                sh "sudo docker compose up -d"
            }
        }
    }
}
