1. What is Jenkins, and how is it used in CI/CD?
Jenkins is an open-source automation server used to build, test, and deploy software automatically.
In a CI/CD pipeline, Jenkins automates the steps such as:

Pulling code from Git

Building the application

Running tests

Packaging (e.g., creating Docker image)

Deploying to staging/production

It integrates with many tools like GitHub, Docker, Kubernetes, Ansible, AWS, etc.

2. What is a Jenkinsfile?
A Jenkinsfile is a text file that contains the pipeline as code, written in either declarative or scripted syntax.

It defines:

The stages (e.g., build, test, deploy)

The steps inside each stage

The use of environment variables, credentials, Docker, etc.

✅ It helps in version-controlling the pipeline along with your source code.

Example:

groovy
Copy
Edit
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
}
3. How do you create and configure Jenkins pipelines?
There are two ways:

✅ Using GUI (Freestyle or Pipeline Job):

Go to Jenkins dashboard → New Item → Pipeline

Configure the Git repo, credentials, and Jenkinsfile location.

✅ Using a Jenkinsfile from Git repo:

Create a file called Jenkinsfile in your repo.

In Jenkins, point the pipeline job to that repo.

Jenkins will automatically use the Jenkinsfile for execution.

4. What are some common stages in a Jenkins pipeline?
Typical stages include:

Checkout: Clone the code from Git

Build: Compile the code or build a Docker image

Test: Run unit/integration tests

Package: Create a deployable artifact (e.g., .jar, .zip, Docker image)

Deploy: Push to DockerHub, AWS, or deploy to Kubernetes

Notify: Send Slack/Email notifications

5. What is the difference between a declarative and scripted Jenkins pipeline?
Feature	Declarative Pipeline	Scripted Pipeline
Syntax	Simple and structured	Full Groovy scripting
Readability	Easier to read and write	More flexible but complex
Example	pipeline { ... }	node { ... }
Use Case	Beginners or standard pipelines	Complex logic or advanced flows
Error Handling	Built-in	Needs manual try-catch

