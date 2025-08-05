<img width="1362" height="717" alt="output-image" src="https://github.com/user-attachments/assets/7eeea8e8-38ae-449a-bad9-e7ef83555923" />
python flask app
This project implements Jenkins CI/CD for a python based application

Overview:
Create a Simple Jenkins Pipeline for CI/CD

Steps followed :

Step1 : Clone the Repository
git clone https://github.com/Harshithaa-K/ELEVATE-TASK-DAY-2.git
cd ELEVATE-TASK-DAY-2

Step 2. Dockerize the Python App

FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
COPY app.py .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]

Step 3 : Configure Jenkins Pipeline
Create a new Jenkins Pipeline Job
Add Jenkins credentials for DockerHub 
Install Docker pipeline plugin

pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('my-dockerhub-token') // Replace with your Jenkins Credentials ID
        IMAGE_NAME = 'harshithagowdam/my-app'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/Harshithaa-K/ELEVATE-TASK-DAY-2.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'my-dockerhub-token') {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying container...'
                sh """
                    docker stop my-app || true
                    docker rm my-app || true
                    docker run -d --name my-app -p 5000:5000 ${IMAGE_NAME}:latest
                """
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}

Step 4 :
Run the Jenkins Pipeline
Clicked Build Now
Jenkins will Clone the repo , Build Docker image , Push to DockerHub , Deploy container locally.
Build logs attached in the repository.

Step 5 :
Accessed the App in Browser using http://<public_ip>:5000


<img width="1366" height="768" alt="Screenshot (41)" src="https://github.com/user-attachments/assets/793dca07-764c-455a-84a6-53cd99cda903" />





