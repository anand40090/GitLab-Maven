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

