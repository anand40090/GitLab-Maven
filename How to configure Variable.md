GitLab CI's Variables system lets you inject data into your CI job environments. 
You can use variables to supply config values, create reusable pipelines, and avoid hardcoding sensitive information into your .gitlab-ci.yml

## How to set environment variables / Plugins :

- Defining a Variable
  
Variables are created on the Settings > CI/CD > Variables screen of the scope you want them to be available in. 
For a project-level variable, that means going to Settings > CI/CD from GitLab's left sidebar while viewing a page within the project. 
Similarly, for group-level variables, navigate to the group and use the sidebar to reach its CI settings. 
Instance-level variables are located via the same route in the GitLab Admin Area.


![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/cf3dfb60-f756-4ec0-9733-66f90b7ced40)

Each variable needs a unique Key; this is how you'll reference the variable within your pipeline and its scripts. The name you choose must be compatible with the shell that'll run your job - if you pick a reserved keyword, your job could fail. All variables should be a valid string containing only alphanumeric characters and underscores.

Next set the value of your variable. When the "Type" dropdown is left at "Variable," this value will be injected as-is each time you reference the variable in your pipeline. 
Changing the type to "File" will inject the value as a temporary file in your build environment; the value of the environment variable will be the path to that temporary file. 
This can be a safer way to inject sensitive data if your application is prepared to read the final value from the specified file.

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/b21e35bf-71cb-4613-8721-c5f46ef58e0c)

Once you're done, click the green "Add variable" button to complete the process. 
You can now reference your variable in pipelines that execute within the scope you defined it in. 
For a project variable, it'll be defined for pipelines inside that project, whereas instance-level variables will be available to every pipeline on your GitLab server.
Variables can be managed at any time by returning to the settings screen of the scope they're set in. 
Click the Edit button (pencil icon) next to any variable to display the editing dialog and change the variable's properties. This dialog also provides a way to delete redundant variables.

## Masked Variables

The "Mask variable" option is another way to enhance the safety of your variables. 
When this checkbox is enabled, GitLab will automatically filter the variable's value out of collected job logs. 
Any unintentional $SECRET_VALUE will be cleaned up, reducing the risk of a user seeing a sensitive token value as they inspect the job logs using the GitLab web UI.

## Environment-Level Variables

Variables can be assigned to specific environments. 
This feature lets your pipelines operate with different configuration depending on the environment they're deploying to.

Use the "Environment scope" dropdown in the "Add variable" dialog to select an environment for your variable. 
The variable will only be defined in pipelines which reference the selected environment via the environment fields in the .gitlab-ci.yml file.

Variables can be set at the pipeline level with a global variable


# GitLab-Maven
This project is for GitLab Maven Integration for Java SpringBopot application.
First create Gitlab account and have one AWS EC2 ubuntu instance. 
Install the required softwares on the EC2 instance and configure the gitlab runner on it to accomodate the gitlab runner. 
Create gitlab project and upload your project on that reposiroty. 


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
Create project on the created gitlab account to configure Ci-CD jobs and pipelines. 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/511cab19-d3e2-4ba8-9ec7-3c8f07961820)

Once the gitlab account is created, create a new project 

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/3be06e67-1fa5-4fbb-945e-4b807ee9a7ff)

   
## Install GitLab Runner on Ubuntu 20.04 LTS

To run the Gitlab CI-CD jobs, gitlab runner is required. 
In this lab we are using AWS EC2 Ubuntu instance to have gitlab runner configuration. 
To install Gitlab Runner on Ubuntu instance follow the steps mentioned below - 

Step 1: Add the Official GitLab Repository on EC2 Ubuntu instance 

First add the official GitLab Repository using below command, to check latest Gitlab Repository visit the official GitLab Runner page
'''

curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash

'''

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/d22c0a2e-5050-4041-9176-e46a686e30f5)


Step 2: Install GitLab Runner on Ubuntu

```

Run below command to install latest GitLab Runner on Ubuntu 20.04 LTS

sudo apt-get install gitlab-runner

To check status if GitLab Runner service is running or not

sudo gitlab-runner status

Commands to Start, Stop and Restart GitLab Runner

sudo gitlab-runner start

sudo gitlab-runner stop

sudo gitlab-runner restart

```

![image](https://github.com/anand40090/GitLab-Maven/assets/32446706/84433f7b-a10c-48e6-838a-f2972a34c9f4)




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
