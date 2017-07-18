# ORACLE Cloud Test Drive #
-----
## 102: Define Continuous Integration 'Build' and 'Deploy' Configuration in Oracle Developer Cloud Service ##

### Introduction ###
This tutorial demonstrates how to:
- Deploy Loyalty Management application to Java Cloud Service using Oracle Developer Cloud Service
The Loyalty Management application is a JEE web application which is built by simple JSP pages, to serve marketing manager for offer campaign creation.  

### About the Exercise Today ###
In this exercise, we will:
- Configure Build Job for the Loyalty Management - A JEE application
- Configure Java Cloud Service - WebLogic Server deployment in Developer Cloud Service
- Build and Deploy Loyalty Management Application using Developer Cloud Service

### Prerequisites ###
+ Oracle Public Cloud Service account including Developer Cloud Service and Java Cloud Service
+ [Create Oracle Developer Cloud Service project for Loyalty Management JEE application](101-JavaAppsLab.md)

----

#### Open Oracle Developer Cloud Service Project ####

1. [Sign in](sign.in.to.oracle.cloud.md) to [https://cloud.oracle.com/sign-in](https://cloud.oracle.com/sign-in) by provided **Developer Cloud Service \(DevCS\)** identity domain Id and credential. First select your datacenter then provide the identity domain and credentials. After a successful login you will see your Dashboard. Find the Developer Service tile and click the hamburger icon. In the dropdown menu click **Open Service Console**.

![](images/102/01.dashboard.png)

2. Select your Oracle Developer Cloud Service Project which was created using initial Git repository and contains Loyalty Management application's sources.

![](images/102/20.open.devcs.project.png)

### Configure build job for Loyalty Management application ###

3. Once the project provisioning is ready let's create the build job to compile and package the Loyalty Management - JEE application to the desired format for Java Cloud Service.

4. Select **Build** item on the left side menu and click the **New Job** button.

![alt text](images/102/05.new.job.png "Create new build job")

5. Enter name **LoyaltyManagementBuildXX** for the new job, where **XX** is your group number (01-03). Please contact the instruction if you don't know your group number. Select the *Create a free-style job* option and save.
On the Main configuration page of the newly created job make sure **Default (The default Java version in the executing environment)** is the selected JDK.

**REMEMBER to add XX at the end of the job name**

![alt text](images/102/06.job.main.png "Configure job")

6. Change to the **Source Control** tab and select **Git**.
In the git's properties section select the only one available Git repository which is provided in the list.
In the Branches section, add and select **master** option in the list. This is to make sure only **master** branch version will be used.
Leave the advanced settings default.

![alt text](images/102/07.job.scm.png "Configure source control")

7. Click **Triggers** tab to configure *SCM polling*. Select **Based on SCM polling schedule**. This ensures if any files in the source code repository has changed then the build will be fired.

![alt text](images/102/07.scm.trigger.png "Configure source control")

8. Change to **Build Steps** tab and add **Maven 3** build step. Enter **clean install** as Goals and **loyalty/pom.xml** to POM File field. (In case if Build Steps tab just shows **Loading...** for a long time, save the Build configuration then re-open and continue.)

![alt text](images/102/08.job.maven.png "Add build step")

9. Finally change to Post Build tab and check in the **Archive the artifacts** option. Enter **loyalty/target/\*.war** into **Files To Archive** field.

![alt text](images/102/09.job.post.png "Post build")

10. Click on **Save** to update the new job configurations. To check the build job click on **Build Now** on the job's detail page. Once the job is done check the archived artifacts. It should be the following: `loyalty.war`

![alt text](images/102/10.build.artifacts.png "Build artifacts")

Please note the build job contains an extra build step which packs the master loyalty management webapp source artifact into a JEE Web Application Archive (WAR) file loyalty.war. This archive is the desired format to deploy a Java Web application to JCS.

### Configure Java Cloud service deployment ###

11. Now create deployment configuration which enable direct deployment to Java Cloud Service after a successful build job.
Change to **Deploy** page in DevCS and create **New Configuration**

![alt text](images/102/11.new.deploy.png "New deploy configuration")

12. Set the following properties.

- **Configuration Name**: any name to identify deployment configuration - we use **loyaltyXX**, where XX is your group number (01-03).
- **Application Name**: application name in JCS. This will determine the application's URL context path - we use **loyalty**.
- **Deployment Target**: click **New** and select Java Cloud Service and define connection properties such as **Version**, **Protocol**, **Host**, **HTTPS Port** and **credentials**.
  [\(Find out the Java Cloud Service Host and HTTPS Port.\)](java.cloud.md).
  Java Cloud Service - WebLogic Admin Username and Password should be provided by instructor separately.
- **Type**: select **Automatic** which means auto deploy after a successful execution of the build job. Select your previously created job and its artifact to deploy.
- **Job**: The **LoyaltyManagementBuild** Build Step defined in early stage of this lab.
- **Arifact**: **loyalty/target/loyalty.war**, this is the only option available after **Job** is selected.

![alt text](images/102/12.deploy.config.png "Deployment Configuration")

![alt text](images/102/13.jcs.config.png "JCS Configuration")

13. Click **Save**.

### Build and deploy the Loyalty Management Application ###

14. To initiate a deployment to Java Cloud Service now there are two options. You can Start deployment process using the newly created Deployment configuration. Click gear icon and select **Start**.

![alt text](images/102/14.deploy.start.png "Deployment Start")

15. Other option is to fire a new Build Job execution which will deploy artifact after a successfull build. Go back to **Build** page and click the wrench icon belongs to Loyalty Management application build job.

![alt text](images/102/15.build.now.png "Build Now")

16. Both way deploys JEE application on Java Cloud Service. You can check the deployment result on the **Deploy** page. Once the deploy is ready (this may take a while) click the **Deploy to JCS** link.

![alt text](images/102/16.deploy.ready.png "Deploy ready")

17. This opens the WebLogic Server Administration Console. Login with provided WebLogic Admin Username and password.

![alt text](images/102/17.jcs.console.png)"WebLogic Console")

18. Once logged on, click **Deployments** on left navigation menu. You should see your Loyalty Management application **loyalty** in the Summary of Deployments list.

![alt text](images/102/17.deployment.png "Deployments")

19. The Loyalty Management application URL should be in the format of:  
    `https://**<JCS WLS instance IP Address>**/loyalty/jsp/welcome.jsp`, the JCS WLS instance IP address is the same as **Deploy to JCS** target in DevCS at step 12.

![alt text](images/102/18.sample.app.png "Loyalty Management Application")

20. There are many other options to trigger this deploy process. For example build can be triggered by source changes or can be scheduled to specific time of the day.  
    You have finished this lab section.

[Procced to Next - 103: Continuous Integration & Delivery (CICD): Using Eclipse IDE, Commit and Push Code Change to Oracle Developer Cloud Service](103-JavaAppsLab.md)

or

[Back to JavaAppsLab Home](README.md)
