# JENKINS PIPELINE FOR PYTHON IN DOCKER ENVIRONMENT
## Tech stack description

# *Jenkins*
Jenkins is an open-source automation tool that helps automate various stages of the software development lifecycle. It allows developers to define and execute pipelines, which consist of a series of steps to build, test, and deploy applications.

Jenkins can be runned in a local environment with web interface. We can build, test, deploy our code connecting dots to our project!!
* Steps to use Jenkins*
+ Install jenkins in your system through war file or msi file
+ Launch the Jenkins web interface by navigating to http://localhost:8080 in your preferred web browser.
+ Follow the on-screen instructions to complete the Jenkins setup wizard.
+ Install any required plugins for your project by going to "Manage Jenkins" > "Manage Plugins" > "Available" tab.

# *Docker*
Docker is an open-source platform that enables developers to automate the deployment and management of applications using containers. Containers provide a lightweight and portable environment for running applications and their dependencies.

We can run complex applications using containers making ease of availability and accessibility of many applications.

# Project Overview
> TO build a jenkins pipeline for building and testing python code inside a docker container

## Step - 1
***Setting up Jenkins inside Dockers***
+ Install Docker Desktop in your system.
+ Open powershell and type docker to check the working of dockers
+ Run the following command to pull the jenkins image and run it inside a container
  ``` Docker
   docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home <image_name_or_id>
  ```
+ This command will set-up jenkins environment, provides a access password to setup jenkins account.
+![Screenshot (19)](https://github.com/JyothiKumar03/Cloud-projects/assets/88045362/4f85df30-5d91-48a6-addc-a3dc2c3ba4e6)
+![Screenshot (20)](https://github.com/JyothiKumar03/Cloud-projects/assets/88045362/bfd4744d-0d72-41dd-b2c6-f2fe5f969a43)
+ Now, we can open jenkins on local host
+ ![Screenshot (21)](https://github.com/JyothiKumar03/Cloud-projects/assets/88045362/e914c8ed-fe9c-4913-9c2b-8087a5d8374e)
+ Setup your account with the access-password, and then you will be taken to plugins dashboard
+ Click on install basic plugins, wait till all plugins gets installed
+ ![Screenshot (22)](https://github.com/JyothiKumar03/Cloud-projects/assets/88045362/0129f00f-33af-438d-8f58-b914f0078557)

Jenkins setup is done !!

## Step - 2
***Building a pipeline for python script***
+ Click on new Item, click on build pipeline.
+ Give it a name, now we need to add few stages on our project
+ Have a simple python script and a test script using pytest

``` python

```






  
