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
        stage("Deploy"){
            steps {
                echo "Deploying the container"
                sh "docker compose down && docker compose up -d"
            }
        }
        
    }
}
