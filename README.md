# GitLab - Maven End to End CI -CD pipeline

In this lab we would be doing maven project intitrgaion with gitlab. 
To do this lab you would need - 
1. Gitlab Account
2. EC2 instance
3. Maven project
4. AWS ECR reposiroty
5. Sonarqube scanner 

___

## First create EC2 instance and install the required software on it - 

```
Install apache maven >> sudo apt install maven -y

Install Docker engine >> sudo apt install docker.io -y

Install Openjdk >> sudo apt install openjdk-11-jdk -y

Install gitlab runner >>

curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
sudo apt-get install gitlab-runner -y

Install AWS CLI >>

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" 
sudo apt install unzip
unzip awscliv2.zip 
sudo ./aws/install

Run the sonarqube docker container >> docker run -d -p 9000:9000 sonarqube

```

## Create Gitlab account 

Go to https://gitlab.com/users/sign_up to create Gitlab account. 
Once the account is created, you can use for CI-CD pipeline deployment with various stages, tools and plugins. 
Create project on the created gitlab account to configure Ci-CD jobs and pipelines. 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/511cab19-d3e2-4ba8-9ec7-3c8f07961820)

Once the gitlab account is created, create a new project 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/3be06e67-1fa5-4fbb-945e-4b807ee9a7ff)

## Register gitlab runner with the above created EC2 instance 
 
1. First got to gitlab account >> project >> setting >> CI- CD >> search for runners >> expant and click on new runner

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/84902b1b-8b27-47ad-a252-db152b239ed1)

2. Select runner platform Linux >> give name of the runner >> click on create runner

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/404d9095-29cd-477d-93c0-4e94548089d9)

3. You will get gitlab token for runner registretion, follow the commands on the Ec2 instance in order to regiter it with gitlab as a runner worker

```
To register runner >> gitlab-runner register  --url https://gitlab.com  --token glrt-tYK95Ynj6qTBsLtw6vbM

Select the executor when it will prompt for >> shell

To run the runner once registration >> gitlab-runner run

```

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/321ce5af-4a5f-4921-aeb3-a69e5f59969a)

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/1e16cf75-c70c-43bf-92ac-f391ec6c215a)

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/b85f7116-3a1d-4828-b29e-0a81ac9923a3)

Once the runner is properly regitered it will reflect in the same page 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/5e78981d-7013-4d82-a9a7-3d48a06d3eb4)



## Clone the Gitlab project reposiroty to upload the project 

Once the Ec2 instance is ready to work as a gitlab runner worker, 
then clone the gitlab project with your local system from where you need to upload your project data for CI-CD piple build. 

Copy the gitlab project url >> Got to Gitlab project >> Find the Clone with HTTPS option >> copy the URL and clone with your EC2 instance or local system from where you want to upload the project data. 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/e7f5fdf4-61e4-4b1e-9307-5a15726b320d)

```

To clone the gitlab repository >> git clone https://gitlab.com/anand40090/springboot.git
It will craete the springboot folder in your system, save your project data into it and keep it ready to be uploaded on gitlab reposiroty.

To add your project data to commit on gitlab reposiorty >> go to project springboot project folder >> git add *

To commit the project data on gitlab repository >> git commit -m '1st commit'

To push the data to gitlab repository >> git push >> input username password when it will prompt for authentication 
 
```
![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/c2c58464-e1b4-4053-a09f-8d2dc4ef2ac2)


![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/8dcbe0c1-689e-4bd0-8c3d-1a934612b24f)

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/72ad2996-20ae-4b61-ba40-41e8e8f80fba)

## Configure sonarqube to intigrate with Gitlab 

1. At very bigining we have already downloaded the sonarqube docker image and spined the container of port 9000, by running commnd "docker run -d -p 9000:9000 sonarqube"
2. Run docker ps -a coommand on the Ubuntu system to check the docker container status of Sonarqube
3. Use the EC2 Ubuntu instance ip address:9000 in browser to access the sonarqube dashboard
4. Default username and password for sonarqube is admin / admin
5. Generate the token from sonarqube for integration with gitlab >> Login sonarqube >> Go to My Account >> Security >> Generate Token
6. Save the generated token to be hardcode in Gitlab variable



![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/1eb22d7f-77da-4fe3-b8fa-c0aae0f9a7b9)



![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/05895dd3-a945-4631-85e0-6a51f58e6f39)


## Intigrate Sonarqube with Gitlab 

1. Login to gitlab account >> go to project >> go to setting >> CI-CD >> Find for variables >> Expand
2. Create two variable - 1] SONAR_TOKEN >> Input the token generated from sonqrqube 2] SONAR_HOST_URL >> Input your sonarqube URL (http://13.126.187.216:9000/)

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/09f2926d-e96a-48f7-acd4-2397b811f207)


![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/5f6c7ffd-aa5d-40ad-966b-3d69d43184d3)



## Create .gitlab-ci.yml file in the gitlab project reposiroty to run the CI-CD pipeline 

Got to gitlab project >> create the .gitlab-ci-.yml file 

Once this file is created and commited over the gitlab project, it will trigger the CI-CD pipeline and start the stages as mentioned in the file. 

Here we are doing 3 stage CI-CD pipelien - 

1. Build the maven project
2. Test the built maven project
3. Build the docker image from the JAR file which is created while maven project build 

```

variables:
  MAVEN_OPTS: -Dmaven.repo.local=.m2/repository

image: maven:latest

stages:
    - build
    - test
    - package
    - deploy


cache:
  paths:
    - .m2/repository
    - target

build_job:
  stage: build
  tags:
    - docker 

  script: 
    - echo "Maven compile started"
    - "mvn compile"


test_job:
  stage: test
  tags:
    - docker 

  script: 
    - echo "Maven test started"
    - "mvn test"

package_job:
  stage: package
  tags:
    - docker 

  script: 
    - echo "Maven packaging started"
    - "mvn package"


Deploy_job:
  stage: deploy
  tags:
    - docker 

  script: 
    - echo "Maven deploy started"


```

Output when you commit the .gitlab-ci.yml file, it will triger the jobs 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/9797d4fc-8e88-4984-9655-1f3d2bccef11)
