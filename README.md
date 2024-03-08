# GitLab-Maven
This project is for GitLab Maven Integration for Java SpringBopot application

## High Level Steps 
1. Create GitLab Account
2. Create EC2 Instance and install the required applications in it (Git, Docker, Maven, GitLab Runner)
3. Register GitLab Runner
4. Create AWS Registery (ECR) and intigrate it with GitLab to store the docker image 

Reference - 
1. [How to Build Java Project using Maven in GitLab CI|Install GitLab Runner on Ubuntu 22.04 LTS| GitLab](https://youtu.be/yz8Hlwvc3Ek?si=VuDN8tsUNViFe6Qh)
2. [Build Java Project using Maven in GitLab CI/CD](https://www.fosstechnix.com/build-java-project-using-maven-in-gitlab-ci-cd/)
   
## How to Install GitLab Runner on Ubuntu 20.04 LTS

Step 1: Add the Official GitLab Repository

First add the official GitLab Repository using below command, to check latest Gitlab Repository visit the official GitLab Runner page
'''
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
'''

Step 2: Install GitLab Runner on Ubuntu

Run below command to install latest GitLab Runner on Ubuntu 20.04 LTS
'''
sudo apt-get install gitlab-runner
'''

To check status if GitLab Runner service is running or not
'''
sudo gitlab-runner status
'''

Commands to Start, Stop and Restart GitLab Runner

'''
sudo gitlab-runner start
sudo gitlab-runner stop
sudo gitlab-runner restart
'''

## How to Register GitLab-Runner

Step 1: To Register GitLab-Runner run the below command:
'''
sudo gitlab-runner register
'''

Step 2: Then enter the URL and Registration Token from GitLab Account

- Go to the GitLab Account
- Click on Project
- Then click on setting and in below click on CI/CD
- Click on Runner Expand  scroll down and copy URL and registration token And paste on command

Step 3: Then you can give any meaning full description

Step 4: Then Enter tags for the runner (any tag)

Step 5: Then choose any executor – shell , ssh , docker , etc.

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/5e5e2063-80e7-4833-94b7-99f481e24692)

Once you registered Runner for project then you will get runner as below,

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/c8f36501-1a92-4008-8d8f-41858278885e)

