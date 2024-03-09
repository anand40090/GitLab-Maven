# GitLab-Maven
This project is for GitLab Maven Integration for Java SpringBopot application

Prerquistes - 
1. Gitlab account
2. EC2 Ubuntu Instance with softwares Apache maven, Docker engine, Git, Openjdk Java
3. Gitlab Runner 
4. Maven Project for deployment
5. ECR or Docker hub credentials to save the docker image

Reference - 
1. [How to Build Java Project using Maven in GitLab CI|Install GitLab Runner on Ubuntu 22.04 LTS| GitLab](https://youtu.be/yz8Hlwvc3Ek?si=VuDN8tsUNViFe6Qh)
2. [Build Java Project using Maven in GitLab CI/CD](https://www.fosstechnix.com/build-java-project-using-maven-in-gitlab-ci-cd/)


## Create GitLab Account

Go to https://gitlab.com/users/sign_up to create Gitlab account. 
Once the account is created, you can use for CI-CD pipeline deployment with various stages, tools and plugins. 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/511cab19-d3e2-4ba8-9ec7-3c8f07961820)

   
## How to Install GitLab Runner on Ubuntu 20.04 LTS

To run the Gitlab CI-CD jobs, gitlab runner is required. 
In this lab we are using AWS EC2 Ubuntu instance to have gitlab runner configuration. 
To install Gitlab Runner on Ubuntu instance follow the steps mentioned below - 

Step 1: Add the Official GitLab Repository on EC2 Ubuntu instance 

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

## Register GitLab-Runner on EC2 Ubuntu Instance 

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

## Install the required softwares on the GitLab runner EC2 instance 

In this lab we would be using Apache Maven, OpenJdk, Docker. 

```
To install apache maven

sudo apt install maven -y

To install openJdk

sudo apt install openjdk-11-jdk -y

To install Docker engine

sudo apt install docker.io -y 
```
