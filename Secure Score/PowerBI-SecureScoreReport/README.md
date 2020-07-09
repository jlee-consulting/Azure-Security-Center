# Secure Score Over Time Reports

**Secure Score Over Time** is a PowerBI template app that will help you track your security health by monitoring the secure score of your Azure Security Center monitored resources over time, and your resources’ health. 

The template app contains out-of-the-box reports that will help you analyze your security status by providing the necessary information to investigate changes in your score over time.  

## Prerequisite:

1. Power BI account (to open the report as template app you need Pro account).

2. Use [Get-SecureScoreData](https://github.com/Azure/Azure-Security-Center/tree/master/Secure%20Score/Get-SecureScoreData) playbook to export your data. This Logic App playbook exports your secure score and recommendations data every 24 hours to a Log Analytics workspace. The playbook uses a Managed Identity, so assign reader permissions to all the subscriptions or management groups you want to include in the reports. The required steps for assigning a Managed Identity are detailed in the playbook’s README file. 

## **Getting the reports**
You can open the reports with two different options:
1. With Power BI Desktop (described under section *Open with Power BI Desktop*).
2. With Power BI Service (described under section *Open with Power BI Service*).

## Open with Power BI Desktop
1. Download the file *Secure Score Report* from the repository.
2. Open the file using Power BI Desktop.
3. Enter your Log Analytics workspace id and click **Load** button.
![Enter log analytics id](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/LogAnalyticsIdDesktop.png?raw=true)
4. Perform authentication using organizational account with **OAuth2** as the authentication method.  ![Authentication](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/Authentication2.png?raw=true)

5. After authentication completed, the data will be loaded.  
***Note:**  
You can connect your data only if the data already available at the Log Analytics workspace. You can check it by running “SecureScore_CL” in the Log Analytics. Only after you get results to this query you can connect your data.*
6. Publish the report to your Power BI Service. You are now ready to analyze your secure score data over time. 

## Open with Power BI Service

Using this option you will create a Power BI application based on our template app. Please make sure you have Power BI Pro account before starting the process.

1. Go to [this](https://msit.powerbi.com/groups/me/apps/0c3bbb94-36cc-4153-a5c2-b63181a17166/package/14ec9028-3513-4a1c-aed1-83a01ecfc975qTsHacSHROKH9oDSq9Co9Ln72xYehlJKmEvIYPIxbz8/install?ownerId=72f988bf-86f1-41af-91ab-2d7cd011db47&referrer=frc-word-edit.officeapps.live.com) link.
2. Click **Install** button as shown in the example below: 

    ![Install app](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/InstallTemplateApp.png?raw=true)

    *In case you are getting ‘This app hasn’t been listed on AppSource. You don’t have permissions to install this app’ message, make sure the option to install template apps not listed in AppSource is enabled in the admin portal (default value is disable).*
    ![Install app problem](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/InstallingProblem.PNG?raw=true)
3.	Choose workspace name and click **Continue** button as shown in the example below:
![Choose workspace](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/ChooseWorkspace.png?raw=true)
4. After the installation is completed, a new app should be added to your apps. Click on your new app.
![New app](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/AppAfterInstalling.png?raw=true)

5. You have now three options, as shown in the example below: 
    1. **Connect to your own data:** Connect directly to your Log Analytics workspace. 
    2. **Explore with sample data:** You can use this option before exporting the data to Log Analytics workspace to explore the app capabilities. When you’re ready to connect to real data click ‘Connect your data’ on the top message. 
    3. **Customize and share:** Customize the reports or create new reports in the app. You can return to this option later by changing the reports in your workspace and click “Update app” button. 
    
    ![Template app options](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/TemplateAppOptions.png?raw=true)

### **Connect to your own data**
1. Enter your Log Analytics workspace id and click **Next** button. 

    ![Enter log analytics id](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/LoAnalyticsIdService1.png?raw=true)

    You can find the id in the Log Analytics workspace overview in the portal, as shown the example below: 
![How to get workspace id](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/LogAnalyticsIdService2.png?raw=true)

    ***Note:**  
    You can connect your data only if the data already available at the Log Analytics workspace. You can check it by running “SecureScore_CL” in the Log Analytics. Only after you get results to this query you can connect your data.*
2. Perform authentication using **OAuth2** as the authentication method and **Organizational** as the privacy level, then click **Sign in** button to continue. 

    ![Authentication to service](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/AuthenticationService.png?raw=true)
3.	It may take few minutes for the data to refresh. If the data hasn’t refreshed after 10 minutes, try manually refreshing the page.

You are now ready to analyze your secure score data over time.

## **Reports Content**

The template app consists of two reports: 

1. **Secure Score Summary** provides summarized data regarding your score progress. 
2. **Resources Summary** provides summarized data regarding your resources’ health.  

The reports are based on the data you exported to the Log Analytics workspace only. 

Notice the reports can be filtered by time using the date scroll bar or by subscription name when you want to focus on a specific subscription. The subscriptions filter can filter all visualizations apart from the aggregated score visualizations that always present the aggregated score for all subscriptions. 

### **Secure score summary report**: 

* **Current aggregated secure score** – Aggregated score for all subscriptions based on the number of resources in each subscription. 
* **Aggregated secure score over time** – Aggregated score over time for all subscriptions to detect aggregated changes in your organization score. 
* **Secure score over time per subscription** – Secure score over time to detect changes in the score for each subscription separately.  
* **Controls score over time** – Security controls score over time to detect changes on a specific control.  
* **Score trends per subscription** – Present the current score for each subscription and total score change in the last week and in the last month. 
* **Detected changes that may affected your secure score** – To help you investigate the reasons for increase/decrease in your score, we present every day the changes which potentially affected the score. That includes deleted resources, newly deployed resources and resources with a change in status for one of the recommendations. Note, those changes are not necessarily the reason for the score change. Also note that it may take up to 24 hours for changes to appear. 

 ![Secure score report](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/Report1.png?raw=true)

 

### **Resources summary report**: 

* **Recommendations current state** – Number of healthy, unhealthy and not-applicable resources for each recommendation. 
* **Controls status sorted by potential impact** – Comparison between healthy and unhealthy resources for each control. The controls are sorted by the control max score, to help you focus on the most important controls. 
* **Remediated resources and new unhealthy resources** – In case you saw on the ‘Detected changes that may affected your secure score’ table resources that changed their security status, you can use this table to understand on which recommendation the status was changed, and what was the change. 
* **Unhealthy resources over time per recommendation** – Number of unhealthy resources for each recommendation over time.  
* **Number of healthy vs. unhealthy resources over time** – Total number of healthy and unhealthy resources over time. 

 ![Secure score report](https://github.com/amitmag-ms/Public/blob/master/Azure%20Security%20Center/Secure%20Score/Imgs/Report2.png?raw=true)

## **Send feedback** 

Have you tried the template app? Help us getting better by filling this [form](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR_CzuCpXTVhBswcSTF6htOtUOFNBS1gxQ01BTVIwOElNNldSVllTNTNBNC4u). Your feedback is highly appreciated. 

 

## **Need Help?** 

Please contact: t-ammage@microsoft.com 