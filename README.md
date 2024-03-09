# GitLab - Maven End to End CI -CD pipeline

In this lab we would be doing maven project intitrgaion with gitlab. 
To do this lab you would need - 
1. Gitlab Account
2. EC2 instance
3. Maven project

___

## First create EC2 instance and install the required software on it - 

```
Install apache mave >> sudo apt install maven -y

Install Docker engine >> sudo apt install docker.io -y

Install Openjdk >> sudo apt install openjdk-11-jdk -y

Install gitlab runner >>

curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
sudo apt-get install gitlab-runner -y 

```

## Create Gitlab account 

Go to https://gitlab.com/users/sign_up to create Gitlab account. 
Once the account is created, you can use for CI-CD pipeline deployment with various stages, tools and plugins. 
Create project on the created gitlab account to configure Ci-CD jobs and pipelines. 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/511cab19-d3e2-4ba8-9ec7-3c8f07961820)

Once the gitlab account is created, create a new project 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/3be06e67-1fa5-4fbb-945e-4b807ee9a7ff)

## Register gitlab runner with the above created EC2 instance 

Step 1: To Register GitLab-Runner run the below command:

'''

sudo gitlab-runner register

'''

Step 2: Regiter gitlab runner with Ec2 Instance 

1. First got to gitlab account >> project >> setting >> CI- CD >> search for runners >> expant and click on new runner

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/84902b1b-8b27-47ad-a252-db152b239ed1)

2. Select runner platform Linux >> give name of the runner >> click on create runner

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/404d9095-29cd-477d-93c0-4e94548089d9)

3. You will get gitlab token for runner registretion, follow the commands on the Ec2 instance in order to regiter it with gitlab as a runner worker

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/321ce5af-4a5f-4921-aeb3-a69e5f59969a)

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/1e16cf75-c70c-43bf-92ac-f391ec6c215a)

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/b85f7116-3a1d-4828-b29e-0a81ac9923a3)


## Clone the Gitlab project reposiroty to upload the project 

Once the Ec2 instance is ready to work as a gitlab runner worker, 
then clone the gitlab project with your local system from where you need to upload your project data for CI-CD piple build. 

Copy the gitlab project url >> Got to Gitlab project >> Finf the Clone with HTTPS option >> copy the URL and clone with your EC2 instance or local system from where you want to upload the project data. 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/e7f5fdf4-61e4-4b1e-9307-5a15726b320d)

```

To clone the gitlab repository >> git clone https://gitlab.com/anand40090/springboot.git
It will craete the springboot folder in your system, save your project data into it and keep it ready to be uploaded on gitlab reposiroty.

To add your project data to commit on gitlab reposiorty >> go to project springboot project folder >> run git add *

To commit the project data on gitlab repository >> git commit -m '1st commit'

To push the data to gitlab repository >> git push >> input username password when it will prompt for authentication 
 
```
![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/c2c58464-e1b4-4053-a09f-8d2dc4ef2ac2)


![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/8dcbe0c1-689e-4bd0-8c3d-1a934612b24f)

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/72ad2996-20ae-4b61-ba40-41e8e8f80fba)


