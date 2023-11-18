# CICD INFRASTRUCTURE VOLUNTEER TASK

Jenkins Automated Build and Deployment Documentation
Overview
This documentation outlines the process of automating the build and deployment of an application using Jenkins. In this project, Jenkins is utilized to build a Docker image, push it to DockerHub, and deploy the application on an EC2 instance.

Prerequisites
AWS account
Two EC2 instances running Ubuntu
DockerHub account
Jenkins with GitHub plugin and SSH plugin
GitHub webhook configured
Setup
Set Up Jenkins Environment
Create an EC2 Ubuntu instance (t3 medium) with security group allowing SSH (port 22) and Jenkins access (port 8080).

SSH into the instance and install Docker:

bash
Copy code
sudo apt update
sudo apt install docker.io -y
sudo docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
Access Jenkins by visiting <ip-address-of-your-instance>:8080, retrieve the initial password, and complete the setup.

Jenkins Configuration
Install GitHub and SSH plugins in Jenkins.
Create a pipeline and Jenkinsfile in your GitHub repository.
Configuration
In the Jenkins UI, navigate to "Manage Jenkins" and select "Credentials."
Add three credentials: GitHub, DockerHub, and your EC2 key. These credentials will be used as environment variables in Jenkins during the build.
Integration with EC2
Jenkins integrates with EC2 using the SSH plugin, allowing Jenkins to use the EC2 key pair to access the instance.

Build Process
During the build stage, Jenkins uses DockerHub credentials to access DockerHub. Jenkins checks for the Dockerfile in the GitHub repository and builds the Docker image.

Deployment Process
Jenkins automates the deployment process on an EC2 instance through the SSH agent. The Jenkinsfile specifies the IP address and username of the instance for the connection. Ensure Docker is installed on the target EC2 instance, and DockerHub is logged in.

Testing
No specific testing is implemented in this project. Consider implementing testing procedures as per your project requirements.

Troubleshooting
If encountering Docker permission issues on the Jenkins server, run:
bash
Copy code
docker exec -u 0 -it <container-id> bash
chmod 666 /var/run/docker.sock
Ensure correct security group rules on the EC2 instance.
Ensure Docker is logged in on the target EC2 instance.
Example Usage
[Provide a simple example or use case for the automated build and deployment process.]

Security Considerations
Securely manage credentials in Jenkins.
Regularly update and patch the EC2 instances.
Restrict access to Jenkins and EC2 instances based on security groups and user roles.
Future Improvements
[Recommend future improvements based on your insights and experiences.]

References
[Include any relevant references or external documentation.]

Feel free to adjust the content based on your specific requirements and preferences.





