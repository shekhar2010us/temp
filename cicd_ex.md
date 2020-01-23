## Login to Remote Windows


### 1. Remote Desktop Login credentials

```bash
IP: <provided_ip>
Username: administrator
Password: JustM300
```

This will take you to the remote windows machine.
<br><br>
In the chrome browser, login to the azure devops

### 2. Azure DevOps Login credentials

```browser
URL: https://devopsclassroom.visualstudio.com/
Username: DevOpsStudent@Outlook.com
Password: JustM300
```

This will take you to the home page of Azure DevOps.

<kbd><img src="images/home.png" alt="drawing" width="500"/></kbd>



### 3. Create a Azure DevOps Project

By providing the following attributes

```
Project name: ServiceReservation<your_name>
* choose private *
Version Control: Team Foundation Version Control
Work Item process: Agile
```

<kbd><img src="images/create_project.png" alt="drawing" width="500"/></kbd>


### 4. Add widget

1.	Click on the <b>Dashboards</b> tab, <b>Add Widget</b>, search for <b>Visual Studio Shortcuts</b> and <b>Add</b> it to the dashboard. You may also add couple more widgets in the dashboard.
2.	After adding all widgets, do <b>done editing</b>



### 5. Explore Features
1.	<b>Repos</b> tab.  This is where the source code repository is, the Team Foundation Server version control where you upload code & check it into source control.
2.	<b>Boards</b> tab. This is where all work items are maintained
3. <b>Backlogs</b> menu in the <b>Boards</b> tab. This is where we add new User Stories to our product backlog. This is also where we upload these User stories to the iterations of our sprints.
4. <b>Pipelines</b> tab.  This is where we will create build definitions.
5. There is a <b>Wiki</b> tab in <b>Overview</b>. If we have any issues or information that we want to share with our team, we can create a Wiki here. If we have a new way to automate something that will save everybody time, or we have discovered a more efficient process for product delivery, it can be documented here.


### 6. Create a Build Definition

Go to the <b>Pipelines</b> tab.
<br>Click the **Create Pipeline** button.

#### Where is your code --> Choose **Team Foundation Version Control**

<kbd><img src="images/tfvc1.png" alt="drawing" width="500"/></kbd>

#### Select a source  --> Choose **TFVC** again

<kbd><img src="images/tfvc2.png" alt="drawing" width="500"/></kbd>

#### Select a template --> Search or choose **ASP.NET** project and click Apply

<kbd><img src="images/asp.net.png" alt="drawing" width="500"/></kbd>

The Build Definition Name property will be set to ```Service Reservations {YourName}-ASP.NET-CI``` by default


### 7. Configure the Build Definition

#### 7a. Enable Code coverage

On the **Task** tab, click on **Test Assemblies**. Scroll down until you see the “**Code coverage enabled**” option. Check the corresponding checkbox.
<br>Click the dropdown next to Save and Queue and Select **Save** to save the Build Definition.
Note:- **DO NOT ```Save and Queue```**, the build will fail because you do not have any code yet


<kbd><img src="images/code_coverage.png" alt="drawing" width="500"/></kbd>

#### 7b. Enable CI Build Trigger

Navigate to the **Triggers** tab. Enable the **Continuous Integration Trigger** by flipping the switch under Enable this Trigger that says “Disabled” to the “Enabled” position.


<kbd><img src="images/ci_trigger.png" alt="drawing" width="500"/></kbd>


#### 7c. Enable Gated Checkin Trigger

Navigate to the **Triggers** tab. Enable the **Gated check-in** by checking the box. Leave everything as-is

<kbd><img src="images/gated_checkin.png" alt="drawing" width="500"/></kbd>

<br>Click the dropdown next to Save and Queue and Select **Save** to save the Build Definition.
Note:- **DO NOT ```Save and Queue```**, the build will fail because you do not have any code yet


#### 7d. Enable Bug Task on Build Failure

Navigate to the **Options** tab. Enable **Create work item on failure**. Default option is to create a bug and assign to the requestor, leave as-is

<kbd><img src="images/bug_task.png" alt="drawing" width="500"/></kbd>

<br>Click the dropdown next to Save and Queue and Select **Save** to save the Build Definition.
Note:- **DO NOT ```Save and Queue```**, the build will fail because you do not have any code yet

Finally click on the Pipelines again to see the list of build pipelines. Since the pipeline has not been run yet, it will show ```no runs yet```

<kbd><img src="images/no_runs_yet.png" alt="drawing" width="500"/></kbd>
<br><br>

### 8. Create a new ASP.NET MVC project

1. Go to ```Dashboards```, Under widget Visual Studio, choose the ```Open in Visual Studio``` 
2. If the dialogue box pops up, select ```Visual Studio Version selector```. This will open Visual Studio 2017 in the Windows virtual machine.
3. If it complains about credentials, login using the same credential that you used for azure devops. ```Username: DevOpsStudent@Outlook.com``` and ```Password: JustM300```
4. Click on ```File``` -> ```New Project```
5. Choose ```ASP.NET Web Application (.Net Framework)``` as the framework
6. Name the project ```Service Reservation WebUI```
7. In the Solution name field, ```remove WebUI``` so it reads as ```Service Reservation``` only, and click OK.
8. When the next dialogue box pops up, choose the ```MVC``` option
9. Check the ```Add unit tests``` checkbox
10. Click on the ```Change Authentication``` button, and select the ```Individual user accounts``` option by clicking the radial button. 

*** Make sure you have the **MVC** checkbox & **Add unit tests** checked, and click **OK**


### 9. Run unit test locally

1. **Go to Test** -> **run all test**
2. Go to **Test explorer** -> all three unit test passed


### 10. Register a user
So it will create an entry in the database

1. **Go to IIS Express (Google chrome)**. This will open the app in Google chrome
2. ```Register``` a user -> provide ```email``` and ```password```
3. Close the browser window to stop the debugging


### 11. Configure Build Tools

#### 11a. Review Database Setting in web.config
1. In the ```Service Reservation WebUI``` project, check ```Web.config``` file.
2. Look for a connection object similar to this ```connectionString="Data Source=(LocalDb)\MSSQLLocalDB;AttachDbFilename=&quot;|DataDirectory|\aspnet-Service Reservation WebUI-20200123020255.mdf```, and note down WebUI-20200123020255
3. In the ```SQL Server Object Explorer```, navigate menus under ```localdb``` -> ```databases``` until you reach the same database mentioned in ```Web.config```
4. Once you reach the correct database, right click and ```click new project```
5. Name the database project as ```Service Reservations DB```
6. browse and save it to the same directory where you have ```Service Reservation```.. It might be ```C:\Users\Administrator\source\repos\Service Reservation```
7. 
 
 