# CICD INFRASTRUCTURE VOLUNTEER TASK

# Jenkins Automated Build and Deployment Documentation

![004](https://github.com/bankolejohn/test-task/assets/76499525/4466b5c8-cb2a-4119-88f1-38689ec15dd7)


## Overview
This documentation outlines the process of automating the build and deployment of an application using Jenkins. In this project, Jenkins is utilized to build a Docker image, push it to DockerHub, and deploy the application on an EC2 instance.

## Prerequisites
AWS account
1. Two EC2 instances running Ubuntu
2. DockerHub account
3. Jenkins with GitHub plugin and SSH plugin
4. GitHub webhook 

## Setup
## Set Up Jenkins Environment
1. Create an EC2 Ubuntu instance (t3 medium) with security group allowing SSH (port 22) and Jenkins access (port 8080).
2. SSH into the instance and install Docker:

sudo apt update
sudo apt install docker.io -y
sudo docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

3. Access Jenkins by visiting <ip-address-of-your-instance>:8080, retrieve the initial password, and complete the setup.
4. Set up your security group allow for port 8080

![243234942-8f35d803-eb88-4be7-9925-d15bc6287b59](https://github.com/bankolejohn/test-task/assets/76499525/8637b708-8ef7-4023-8639-b2b0d9bb87a9)
<img width="1091" alt="230627131-aaafa007-69b6-47ac-b656-abd3f507233a" src="https://github.com/bankolejohn/test-task/assets/76499525/acec4960-ff99-4db8-998f-9123e2eac180">
<img width="1409" alt="230627570-b00d52f1-9eba-49d0-a04a-88e465896f2e" src="https://github.com/bankolejohn/test-task/assets/76499525/03e4afce-5db7-4b8f-b4c6-f9edc98247f3">
<img width="1336" alt="230622290-5bb9bae6-2515-4f48-aafa-566fc782073c" src="https://github.com/bankolejohn/test-task/assets/76499525/5f018a61-49f6-4167-81a0-d0af140bfd45">


## Jenkins Configuration
1. Install GitHub and SSH plugins in Jenkins.
2. Create a pipeline and Jenkinsfile in your GitHub repository.

## Configuration
1. In the Jenkins UI, navigate to "Manage Jenkins" and select "Credentials."
2. Add three credentials: GitHub, DockerHub, and your EC2 key. These credentials will be used as environment variables in Jenkins during the build.

## Integration with EC2
Jenkins integrates with EC2 using the SSH plugin, allowing Jenkins to use the EC2 key pair to access the instance.

## Build Process
During the build stage, Jenkins uses DockerHub credentials to access DockerHub. Jenkins checks for the Dockerfile in the GitHub repository and builds the Docker image.

## Deployment Process
Jenkins automates the deployment process on an EC2 instance through the SSH agent. The Jenkinsfile specifies the IP address and username of the instance for the connection. Ensure Docker is installed on the target EC2 instance, and DockerHub is logged in.


## Testing
No specific testing is implemented in this project. Consider implementing testing procedures as per your project requirements.

## Troubleshooting

. If encountering Docker permission issues on the Jenkins server, run:
docker exec -u 0 -it <container-id> bash
chmod 666 /var/run/docker.sock
. Ensure correct security group rules on the EC2 instance.
. Ensure Docker is logged in on the target EC2 instance.

## Security Considerations
1. Securely manage credentials in Jenkins.
2. Regularly update and patch the EC2 instances.
3. Restrict access to Jenkins and EC2 instances based on security groups and user roles.

