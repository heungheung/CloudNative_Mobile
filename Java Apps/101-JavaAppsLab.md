# ORACLE Cloud Test Drive #
-----
## 101: Create Oracle Developer Cloud Service Loyalty Management application project using initial GitHub repository ##

### Introduction ###
This tutorial demonstrates how to:
- Create Oracle Developer Cloud Service project using existing external Git repository - GitHub

### About the Exercise Today ###
In this exercise, we will:
- Create a new Developer Cloud Service Project for the Loyalty Management System
- Create a new Developer Cloud Service Git Repository to store the Loyalty Management Java Application Source Code
- Clone an external Git repository, which is stored in Github, to the Developer Cloud Service Git Repository create above

### Prerequisites ###
- Oracle Public Cloud Service account including Developer Cloud Service (Check with instructor if you don't have one)

### Note
Please be reminded that the screen captures shown below might differ from what you see on your screen - as your Identity Domain Name, Username, **Project Name**, etc can be different.

----

#### Create Oracle Developer Cloud Service project ####

1. Sign in to [https://cloud.oracle.com/sign-in](https://cloud.oracle.com/sign-in) by provided **Developer Cloud Service \(DevCS\)** identity domain Id and credential. First select your datacenter then provide the identity domain and credentials. After a successful login you will see your Dashboard. Find the Developer Service tile and click the hamburger icon. In the dropdown menu click **Open Service Console**.

![](images/101/01.dashboard.png)

2. Log in to Oracle Developer Cloud Service and create a new project.

![alt text](images/101/02.new.project.png)

3. Enter the name of the project and set the desired properties.   
	**Name:** `APAC Cloud Test Drive XX`   
	**Description:** `APAC Cloud Test Drive project hub`   
	where **XX** is your group number - from 01 to 03. Please check with the instructor if you don't know your group number.

** REMEMBER to add XX (your group number) in the project name.**

![](images/101/02.new.project.detail.png)

4. Click **Next** and select *Initial Repository* as template.

![](images/101/03.select.template.png)

5. Click **Next** and on the Properties page select *Import existing repository*.
Enter or copy the *https://github.com/APACTestDrive/LoyaltyManagement.git* repository address.

![](images/101/04.import.repository.png "Import external repository")

6. Now click **Finish** to create the project and to clone the specified repository. You have now created a new Git repository with source code stored within the Developer Cloud Service that is based on an existing repository.

![](images/101/05.new.project.created.png)
![](images/101/05.new.project.created1.png)

You have finished this lab section.

[Procced to Next - 102: Define Continuous Integration 'Build' and 'Deploy' Configuration in Oracle Developer Cloud Service](102-JavaAppsLab.md)

or

[Back to JavaAppsLab Home](README.md)
