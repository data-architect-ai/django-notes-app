pipeline{
    agent any
    
    stages{
        stage("Code"){
            steps {
                echo "Cloning the code"
                git url: "https://github.com/KushalPatel9900/django-notes-app.git", branch: "main"
            }
        }
        stage("build"){
            steps {
                echo "Building the code"
                sh "docker build -t my-notes-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub", passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]){
                sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-notes-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
}
