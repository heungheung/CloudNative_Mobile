Update: July 5, 2017

## 0.1 Introduction

This lab is part of the APAC Cloud Test Drive and is the 2nd lab about creating microservices

## 0.2 Objectives

- Import Code from external Git Repository
- Build and Deploy project using Developer Cloud Service and Oracle Application Container Cloud Services

## 0.3 Required Artifacts

- The following lab requires an Oracle Public Cloud account that will either be applied by yourself or supplied by your instructor.

- You will need to install an IDE environment and GIT client in your local computer. The instructions assume you are using the VM provided as part of this workshop. The VM is also used in the [Oracle DevOps Cloud Native Microservice Workshop](https://github.com/oracle-weblogic/cloud-native-XWeeks/blob/master/cloud-native-devops/README.md). You can download the VM [here](https://drive.google.com/drive/folders/0B0MXC4qaECO6RHBWMEttdW9fOVk).

## 0.4 Notes

The screen captures shown below might differ from what you see in your screen, as the Identity Domain, Username, **Project Name**, etc may be different.

# 1. Create Offer REST API Microservice

## 1.1 Create Initial Git Repository - Offer REST API

- Login to Developer Cloud Service if you haven't done so. If you are in the Cloud Dashboard, you can use Developer Cloud Service Hamburger Menu to navigate to DevCS.

![](images/001.dashboard.png)

- In the left hand navigation panel, click **Project**   
Make sure you are in the correct project, e.g. `APAC Cloud Test Drive XX`, where XX is your group number (01-03).

![](images/002.createrepo.png)

- On the right side in the **REPOSITORIES** section, click on **New Repository** to create a new Git Repository.
- In the New Repository wizard enter the following information and click **Create**.

	**Name:** `OfferMicroserviceXX` where XX is your group number (01-03)

	**Description:** `Microservice to provide REST API of Offer Details`

	**Initial content:** `Import existing repository`

	**Enter the URL:** `https://github.com/APACTestDrive/OfferMicroservice.git`

![](images/003.newrepo.png)

- You have now created a new Git repository stored within the Developer Cloud Service that is based on an existing repository

![](images/004.repo.png)

## 1.2 Create Default Build and Deployment Process - Offer REST API

Now that we have the source code in our Developer Cloud Service managed Git Repository, we need to create a build process that will be triggered whenever a commit is made to the master branch. We will setup a **shell script** build process in this section.

### 1.2.1 Create Default Build Process - Offer REST API

- Click **Build** on the navigation panel to access the build page and click **[+ New Job]**

![](images/005.navibuild.png)

- In the New Job popup window, enter `Offer REST API Build XX` for Job Name (where XX is your group number 01-03) and click **Save**.

![](images/006.newbuildjob.png)

- You are now placed into the job configuration screen.

![](images/007.newjob.png)

- Click the **Source Control** tab. Select **Git** radio button. In the Repositories section, select **OfferMicroservice.git** from the URL drop down.

![](images/008.srcctrl.png)

  **Note:** Make sure you select the Git repository for the Offer REST API Microservice.

- Click **Triggers** tab. Check **Based on SCM polling schedule**.

![](images/009.trigger.png)

- Click the **Build Steps** tab, click **Add Build Step** and select **Execute shell**.

![](images/010.steps.png)

- In the Command textarea, enter: `npm install`

![](images/011.npm.png)

- Click the **Post Build** tab. Check **Archive the artifacts**. For File to Archive, enter `**/target/*` and verify **GZIP** is chosen as the Compression Type.

![](images/012.post.png)

- Click **Save** to complete the configuration.

![](images/013.save.png)

- A build should start automatically within 1-2 minutes. If it does not start automatically, click on the **[ Build Now ]** button.

![](images/014.buildnow.png)

- The status will change to something similar to the following diagrams.

![](images/015.queue.png)

![](images/016.running.png)

- The build will take serval minutes to complete. Wait for the build to complete before continue to the next step - ** as we need the build artifact to create the deployment configuration**.

![](images/017.complete.png)

### 1.2.2 Create Default Deployment Process - Offer REST API

- Click **Deploy** to access the Deployments page and click the **[+ New Configuration]** button.

![](images/018.navideploy.png)

- Enter the following data:

	**Configuration Name:** `OfferAPIDeployXX`, where XX is your group number (01-03)

	**Application Name:** `offerXX`, where XX is your group number (01-03)

![](images/019.deployname.png)

- Next to the right hand side of **Deployment Target**, click the **[New]** button and select **Application Container Cloud...**

![](images/020.deployaccs.png)

- Enter the following information and click **Test Connection**.

	**Data Center:** `your datacenter, e.g. em2, em3, etc`

	**Identity Domain:** `your identity domain`, e.g. gse00012345, etc

	**Username:** `username to login to MyService`, e.g. cloud.admin, john.dunbar, etc - that is the username you are using.

	**Password:** `password of the cloud user`, that is the password you are using

![](images/021.accsconn.png)

- If successful, click **[Use Connection]** button  

![](images/022.useconn.png)

- In the ACCS Properties, set

	**Runtime** to `Node`

 	**Subscription** to `Hourly`

- Set **Type** to `Automatic` and **CHECK** Deploy stable build only

![](images/023.deploynodejs.png)

- Select from the **Job**, this name should match the build job above, e.g. `Offer REST API Build`

- Select from the **Artifact**, this name should match the archive artifact above and the package.json of your source code, e.g. `target/offer.zip`  

![](images/024.deployjobname.png)

- After fill in the above information, click **Save** button.

![](images/025.deploysave.png)

- In your deployment job, click the gear drop down and select **Start**

![](images/026.deploystart.png)

- The deployment job will be put into a queue for process. Wait until the message **Starting application** changes to **Last deployment successded**. Ask for help from your instructor if the deployment fails.

![](images/027.deploysuccess.png)

## 1.3 Login to Oracle Application Container Cloud Service

- Navigate back to the Oracle Public Cloud MyService. Click **Dashboard** to return back to main Cloud Service Dashboard.

![](images/028.dashboard.png)

- On the Application Container Cloud Service (ACCS) click the humburger button and select **Open Service Console**

![](images/029.accsgoto.png)

- On the ACCS Service Console you can view all the deployed applications including our newly create **offerXX**.

![](images/030.accsconsole.png)

## 1.4 Create ACCS Service Binding to DBCS

- Click the **[ offerXX ]** to see the ACCS application Details

![](images/031.accsoffer.png)

- Click the 2nd Tab, **Deployments**

![](images/032.bindings.png)

- In the **Service Bindings** section, click **[Add]** button

![](images/033.addbinding.png)

- Enter the following information

  **Service Type:** `Database Cloud Service`

	**Service Name:** `apacctddbXX`, where XX is your group number (01-03)

	**Username:** `loyalty`

	**Password:** `the database password`, e.g. Welcome_1

 Click **[Save]** button.

**Make sure you SELECT the correct database service, your should use apacctddbXX. Don't use the wrong group!**

![](images/034.addandsave.png)

- Notice that the change is not applied yet. In the **Deployments** dialog, click the **[Apply Edits]** button.

![](images/035.apply.png)

- The change requires redeploying of application. You can navigate back to **Overview** tab and/or use **Refresh** button to check the progress.

![](images/036.redeploying.png)

- Wait until the offer application finish redeployment.

## 1.5 Verify the Working Service

- In you application panel, you should see the base URL of your application. Something like https://offerXX-{your-identity-domain}.apaas.{your-data-center}.oraclecloud.com

![](images/037.url.png)

- Copy and paste the URL into the address bar of a new tab to bring up the application.

  Be reminded that you will need the REST endpoint and the **offer id** in order to generate a QR code.

  The final URL should looks like this

https://offerXX-{your-identity-domain}.apaas.{your-data-center}.oraclecloud.com/ptmgt/v1/offers/10001

![](images/038.browser.png)

- You should be able to get offer details from the Microservice.

![](images/039.result.png)

- Configuration! You've completed the frist microservice. Let's move on the the QR Code Microservice, which is actually very similar to this Part 1.

# 2. Create QR Code Generator Microservice

## 2.1 Create Initial Git Repository - QR Code Generator

- Login to Developer Cloud Service if you haven't done so.
- In the left hand navigation panel, click **Project**

**Make sure you are in the correct project**

![](images/101.project.png)

- On the right side in the **REPOSITORIES** section, click on **New Repository** to create a new Git Repository.

![](images/102.newrepo.png)

- In the New Repository wizard enter the following information and click **Create**.

	**Name:** `QRCodeMicroserviceXX` where XX is your group number (01-03)

	**Description:** `Microservice to generate Offer QR Code. The QR Code will contains an URL of the actual Offer.`

	**Initial content:** `Import existing repository`

	**Enter the URL:** `https://github.com/APACTestDrive/QRCodeMicroservice.git`

![](images/103.repoclone.png)

- You have now created a new Git repository stored within the Developer Cloud Service that is based on an existing repository

![](images/104.repocreated.png)

## 2.2 Modify the sample program code to reflect your own environment

### 2.2.1 Clone Project to Bracket Text Editor

- You can use the Brackets inside the VM as IDE. If you are using other editors / IDE, you will also need to either use command line Git or have Git integration in your IDE. This Lab assume you use Brackets in the VM. This Lab also assume your have direct connection to public Internet, i.e. **NOT behind proxy**

- Start Brackets Text Editor, by right click the **Brackets** desktop icon and select **Open**

![](images/110.startbrackets.png)

- In the **File** pull-down menu, choose **Open Folder**

![](images/111.open.png)

- Click **oracle** in the left hand side and click **[Create Folder]** at the top right hand corner

![](images/112.createfolder.png)

- Enter **QRCodeMicroserviceXX** as the folder name. Then Click any space (e.g. in the size column) next to the name

![](images/113.gotofolder.png)

- Click **[ Open ]** button to open the newly created project folder.

![](images/114.opennew.png)

- Black in **Developer Cloud Service**, in your **QRCodeMicroservice Git Repository**. Click **HTTP** to display the Git HTTP URL, click the **Copy** button to copy the URL.

![](images/115.copyurl.png)

- Back in the Bracket editor, click on **GIT** icon on the right hand side of the editor.

![](images/116.gitbutton.png)

- In the Git panel, click **[ Clone ]**

![](images/117.gitclone.png)

- Paste the GIT URL that you copied from Developer Cloud Service. Username should be populated automatically. Enter the password and select **Save credentials to remote url**

- Click **[OK]** button

![](images/118.gitlogin.png)

- Wait for Brackets to clone your remote project to local folder.

![](images/119.gitwaitclone.png)

- You now have a local copy of the Git Repository.

![](images/120.cloned.png)

### 2.2.2 Edit the source code to fit your environment

- Open the server.js file (double click) in Brackets

![](images/121.openjs.png)

- In line 12, change the URL to your identity domain, i.e. what you have used in **Section 1.5**. As you can see, this is the URL of the **Offer REST API Microservice**. This is the URL we used above, i.e.   
https://offerXX-{your-identity-domain}.apaas.{your-data-center}.oraclecloud.com/ptmgt/v1/offers/

![](images/122.line12.png)

- Save the file. (**Ctrl-S** or choose from pull-down menu **File > Save**)

![](images/123.save.png)

### 2.2.3 Create a new Branch and Commit

- In the left hand navigation panel, select **master** and click **Create new branch...**

![](images/124.branch.png)

- In the pop-up window, enter `ChangeURL` for branch name and click **Ok**

![](images/125.changeurl.png)

- Check the box next to **Commit** to select all modified files - this means the checkbox below (server.js) will automatically be checked.

![](images/126.commitcheck.png)

- Click **Commit**

![](images/127.commit.png)

- In the pop-up enter the **comment** `modify source code to use correct URL` and click **OK**. This will commit the changes to your LOCAL GIT REPOSITORY. (You can ignore the code inspection problems. You can review the code changes before confirmation)

![](images/128.commitmsg.png)

- Click **Git Push** icon.

![](images/129.push.png)

- In the pop-up window, leave all defaults and click **Ok**.

![](images/130.pushok.png)

- Once Git Push completes, click **Ok**

![](images/131.pushdone.png)

- You have push the changes to Developer Cloud Service. If you like, you can go to **Developer Cloud Service** to check the pushed branch. You will something like this.

![](images/132.newbranch.png)

### 2.2.4 create Merge Request in Developer Cloud Service to uptake the code

- In Developer Cloud Service, click on **Code** tab. If you are not viewing the QRCodeMicroserviceXX repo, change to the QRCode Repo.  

![](images/141.checkbranch.png)

- Select ChangeURL branch

![](images/142.changeurlbranch.png)

- Once you are in the ChangeURL branch. You should be able to view the recent commit that we made to branch from Brackets.

![](images/143.changes.png)

- Now, a merge request can be created to merge the code - click on **Merge Requests** to go the merge request panel.

![](images/144.mergereq.png)

- and then click on the **New Merge Request** button.

![](images/145.newmerge.png)

- Enter the following information into the new merge request and click **Next**

	**Repository:** `QRCodeMicroserviceXX.git`

	**Target Branch:** `master`

	**Review Branch:** `ChangeURL`

![](images/146.createreq.png)

- Enter for following information into **Details** and click **Next**

 	**Summary:** `Merge Request for branch ChangeURL`

  **Reviewers:** `Choose the user you are working on` (e.g. Cloud Admin, John Dunbar, etc)

![](images/147.req2.png)

- Review the request and click **[+ Create]** button.

![](images/148.reqcreate.png)

- Now, the merge request has been created. We will approve the request in the next section.

### 2.2.5 Merge the Branch

- click on the **Merge Request**. Select the request we just created and we can review the request.

![](images/151.requestdetails.png)

- Once the request has loaded, select **Change Files** tab. Review the changes. You can add your comment before approve the request.

![](images/152.changedfiles.png)

- if you like you can click the **[Approve]** button to add comments

![](images/153.approve.png)

- Enter some comments, e.g. `approved` and click **OK**.

![](images/154.approvmsg.png)

- You can see the request is now approved by reviewer. Click **Merge** button to proceed merging

![](images/155.clickmerge.png)

- leave the defaults OR enter your desired comment. If you check **Delete branch**, the ChangeURL branch will be deleted after the merging. Click on **Create a Merge Commit** button.

![](images/156.commitmerge.png)

- Now the code merge had been committed and we can build the microservice. 	

![](images/157.merged.png)

## 2.3 Create Default Build and Deployment Process - QR Code Generator

Now that we have the source code in our Developer Cloud Service managed Git Repository, we need to create a build process that will be triggered whenever a commit is made to the master branch. We will setup a **shell script** build process in this section.

### 2.3.1 Create Default Build Process - QR Code Generator

- Click **Build** on the navigation panel to access the build page

![](images/161.navibuild.png)

- Click **[+ New Job]**

![](images/162.createnewbuild.png)

- In the New Job popup window, enter `QR Code Generator Build` for Job Name and click **Save**.

![](images/163.newjob.png)

- You are now placed into the job configuration screen.

![](images/164.buildscreen.png)

- Click the **Source Control** tab. Select **Git** radio button. In the Repositories section, select **QRCodeMicroserviceXX.git** from the URL drop down.

	**Note:** Make sure you select the Git repository for the QR Code Microservice.

![](images/165.srcctrl.png)

- Click **Triggers** tab. Check **Based on SCM polling schedule**.

![](images/166.trigger.png)

- Click the **Build Steps** tab, click **Add Build Step** and select **Execute shell**.

![](images/167.stage.png)

- In the Command textarea, enter: `npm install`

![](images/168.npm.png)

- Click the **Post Build** tab. Check **Archive the artifacts**. For File to Archive, enter `**/target/*` and verify **GZIP** is chosen as the Compression Type.

![](images/169.pb1.png)

- Click **Save** to complete the configuration.

![](images/170.pbsave.png)

- A build should start automatically within 1-2 minutes. If it does not start automatically, click on the **[ Build Now ]** button.

![](images/171.now.png)

- The status will change to something similar to the following diagram.

![](images/172.queue.png)

- building, please wait

![](images/173.building.png)

- The build will take serval minutes to complete. Wait for the build to complete before continue to the next step - ** as we need the build artifact to create the deployment configuration**.

![](images/174.buildsuccess.png)

### 2.3.2 Create Default Deployment Process - QR Code Generator

- Click **Deploy** to access the Deployments page

![](images/181.navideploy.png)

- Click the **[+ New Configuration]** button.

![](images/182.newdeploy.png)

- Enter the following data:

  **Configuration Name:** `QRCodeGeneratorDeployXX`

  **Application Name:** `qrcodegeneratorXX`   

	**REMEMBER XX is your group number (01-03)**

![](images/183.createdeploy.png)

- **As you have created the deployment in the Offer REST API
Microservice, you can REUSE the same target**.

  In the **Deployment Target**, choose the **SAME** one you created above. It should be something similar to `Application Container Cloud` **em2 / your-identity-domain / your-user-name**

![](images/184.dc.png)

- A window **Deploy to Application Container Cloud** will popup, confirm the information and **ENTER the password**, then click **[Test Connection]** button.   

	**Data Center:** `your datacenter, e.g. em2, em3, etc`

	**Identity Domain:** `your identity domain, e.g. gse00012345, etc`

	**Username:** `username to login to MyService, e.g. cloud.admin, etc`

	**Password:** `password of the cloud user`

![](images/185.test.png)

- Once test is success, click **Use Connection**

![](images/186.testgood.png)

- In the ACCS Properties, set

	**Runtime** to `Node`

 	**Subscription** to `Hourly`

- Set **Type** to `Automatic` and **CHECK** `Deploy stable build only`

![](images/187.choosenode.png)

- Select from the **Job**, this name should match the build job above, e.g. `QR Code Generator Build`. Select from the **Artifact**, this name should match the archive artifact above and the package.json of your source code, e.g. `target/qrcodegenerator.zip`  

![](images/188.choosejob.png)

- After fill in the above information, click **Save** button.

![](images/189.depsave.png)

- In your deployment job, click the gear drop down and select **Start**

![](images/190.start.png)

- The deployment job will be put into a queue for process. Wait until the message **Starting application** changes to **Last deployment successded**. Ask for help from your instructor if the deployment fails.

![](images/191.deployed.png)

## 2.4 Login to Oracle Application Container Cloud Service

- Navigate back to the Oracle Public Cloud tab. Click **Dashboard** to return back to main Cloud Service Dashboard.

- On the Application Container Cloud Service (ACCS) click the humburger button and select **Open Service Console**

![](images/192.accs.png)

- On the ACCS Service Console you can view all the deployed applications including our newly create **qrcodegeneratorXX**.

![](images/193.accsqr.png)

- Copy the URL and paste it into the address bar of a new tab to bring up the application.

  Be reminded that you will need the REST endpoint and the **offer id** in order to generate a QR code.

  The final URL should looks like this

	https://qrcodegeneratorXX-{your-identity-domain}.apaas.{your-data-center}.oraclecloud.comm/ctdqr/v1/offer/10001

![](images/194.qrurl.png)		

- the QR Code in the browser will look like this

![](images/195.codepic.png)

- if you use a QR Code reader (e.g. Mobile App), you can decode the QR Code

![](images/196.reader.png)

# Congratulation! You've complete the Microservice Lab.

[go back to the Cloud Test Drive Main Page](../README.md)
