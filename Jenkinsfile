pipeline { 
    agent any 
    
    environment { 
        CONTAINER_NAME = "nestjs-app" 
        IMAGE_NAME = "nestjs-image" 
        EMAIL = "virwalyash@gmail.com" 
        PORT = "3000" 
    } 

    stages { 

        stage("Clone Repo") { 
            steps { 
                git branch: 'main', url: 'https://github.com/Yash-978/CI-CD-Pipelines-Using-Jenkins-GitHub-WebHook-Ubuntu-AWS-EC2-Docker.git' 
            } 
        } 

        stage('Build Docker Image') { 
            steps { 
                sh 'docker build -t $IMAGE_NAME .' 
            } 
        } 

        stage('Stop & Remove Previous Container') { 
            steps { 
                sh ''' 
                    docker stop $CONTAINER_NAME || true 
                    docker rm $CONTAINER_NAME || true
                ''' 
            } 
        } 

        stage('Docker Container Run') { 
            steps { 
                sh ''' 
                    docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME 
                ''' 
            } 
        } 

        stage('Send Email Notification') { 
            steps { 
                emailText( 
                    subject: "NestJS App Deployed Successfully on EC2!", 
                    body: "Your NestJS app is Deployed! http://16.171.254.196:${PORT}", 
                    to: "${EMAIL}"
                ) 
            } 
        } 
    } 
}