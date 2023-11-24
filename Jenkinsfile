pipeline{
    agent  any
    stages{
        stage('Checkout'){
            steps{
                echo "Cloning the code"
                git url:"https://github.com/praveenkuku611/django-notes-app.git",branch:"main"
            }
            
        }
        stage('Build'){
            steps{
                echo "Building the code"
                sh "docker build -t my-note-app ." 
            }
        }
        stage('Push to Docker Hub'){
            steps{
                echo "Pushing the image to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPassword",usernameVariable:"dockerhubUsername")]){
                sh "docker login -u ${env.dockerhubUsername} -p ${env.dockerhubPassword}"
                sh "docker tag my-note-app praveenkuku611/docker-hub-note"
                sh "docker push praveenkuku611/docker-hub-note"
                }
                
            }
        }
        stage('Deploy'){
            steps{
                echo "Deploying the Container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
}
