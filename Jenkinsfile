pipeline{
    agent any
    
    environment{
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "virwalyash@gmail.com"
        PORT = "3000"
    }

    stages{
        stage("Clone Repo") {
            steps{
                git branch: 'main', url: 'https://github.com/Yash-978/CI-CD-Pipelines-Using-Jenkins-GitHub-WebHook-Ubuntu-AWS-EC2-Docker.git'
            }
            
        }

        stage('Build Docker Image'){
            step{
                sh 'docker build -t $IMAGE_NAME .'
                // rememember this . last .
            }
        }

        
        
        stage('Stop & Remove Previous Container'){
            step{
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME
                '''
            }
        }
        
        stage('Docker Container Run'){
            step{
                sh '''
                    docker run -d -p ${PORT}:${PORT}--name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
        
        stage('Send Email Notification'){
            step{
                emailText(
                    
                    subject: "NestJS App Deployed Successfully on EC2!",
                    
                    body: "Your NestJs app is Deployed! http://16.171.254.196:${PORT}",
                    to: "${EMAIL}"
                    // remember this these comas , after the subject body and to


                )
            }
        }
    }
}