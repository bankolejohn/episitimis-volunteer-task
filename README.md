# CICD INFRASTRUCTURE VOLUNTEER TASK

# Jenkins Automated Build and Deployment Documentation

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