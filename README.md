# Sofie Bio Software Standards

## Intro to Software Development Process

This section outlines the life-cycle of the software development process. What is the SOP for receiving/addressing these request changes?

### Change Request

#### Internal Request
Teamwork Projects will be used to create and track SW/UI issues. The following steps will allow the user to create a new
Task and provide the necessary details/images to explain the issue.

##### Reporting In Teamwork Project
1. Login to the SOFIE Teamwork Projects website.
2. Go to the “SW/UI” project within the ELIXYS program.
3. Go to the Task Lists within the “SW/UI” project.
4. Create a Task for the bug/issue in the Task List named “SW/UI Issue Reporting”.
   1. Who and When tab
       1. What needs to be done?
          * Create a brief description
       2. Who should do this?
          * Assign the appropriate person (Alex C. or Justin)
              1. This defines the Owner of the task.
          * Make sure the checkbox for “Notify by Email” is checked and green in color.
          * Start Date and Due Date – Do not fill this out.
   2. Description tab
      1. Write a detailed description of the issue.
   3. Files Tab
      1. Attach any useful logs, data, or images
   4. Priority
      1. Select a priority level based on the severity of the bug/issue.
   5. Followers
      1. Select your name if you wish to follow the progress on this issue.
      
#### Reviewing and assigning priority
1. The Owner of the Task should receive an email alert when a bug/issue task is created.
2. The Owner should review all the pertinent information input into the Task.
    1. Review the Description and any attached Files.
    2. Review the Priority level.
    3. Communicate with the team to make sure all information is complete and the Priority level is appropriate.
3. Update the Priority level and define a Due Date and create a SFDC Case #.
    1. Based on an assessment of the issue, the Owner should edit the Task and assign the appropriate Priority level.
    2. The Owner should enter a Start date and target Due Date for the task.
    3. The Owner should create a SFDC Case # for this task.
4. The Owner should move the Task (issue) into the appropriate Task List.

#### Creating Github Ticket
Once it has been determined that this change requires a code change; a Github ticket shall be created
1. Visit the Issue tab of the Project
2. Select [New Issue](https://github.com/SofieBiosciences/Elixys/issues/new)
    1. Select Assignees
    2. Select Project/Milestone
        1.  If this change will be part of our quarterly schedule select from our Quarterly Milestone
        2.  If this change is immediately required [bug fix]; create a project naming the Third number (revisions) as in vx.y.z.  Still assign the quarterly milestone as this change will be part of that release.
    3. Fill in an appropriate title [Reference the teamwork task id found in the URL https://sofiebiosciences.teamwork.com/#tasks/**4753296**]
    4. Copy the comment from the teamwork task. Reference the teamwork URL in comment
    5. Submit new Issue
    6. Once submitted, the developer shall note all sections that will be affected due to the request change.  It shall be noted in the comment section of github and brought up during Field Service meetings.

#### Working on Completing the task
1.  Create a branch from master on github.  Mention the git ticket name in the bug fix
```
git checkout master
git pull
git checkout -b ticket_name
git push --set-upstream origin ticket_name
git commit -m"Working on ticket #xyz"
git push
```
2. Follow procedure for the type of ticket (C++, python, javascript, css/scss) [See Categorizing Issues & Ticket Types]
3. Once the change has been made, close the github ticket
```
git add all_files_changed
git commit -m"This closes #34, closes #23"
git push
```
4. Validate change has satisfied the creator of the ticket.
    1. Visit the teamwork task id https://sofiebiosciences.teamwork.com/#tasks/**4753296**
    2. Comment to the task creator the fix is ready.  Have the creator validate it fixes their issue.
5. After validating the fix; update src/pyelixys_config.txt
6. Once validated and all tests pass, merge change back to the next release branch
```
git checkout next_release
git pull
git merge ticket_name
git commit -m"Merging #xyz into the next release"
git push
```

#### Deploying the next version
Deploying changes to production will depend on the project.  This document outlines the deployment process for Elixys, as it is our main product.  For SPN deployment procedures, follow Heroku Deployments section in the [SPN README](https://github.com/SofieBiosciences/SPN/blob/master/README.md)

SPN will host all downloadable versions of Elixys.  To view the version list go to https://www.sofienetwork.com/github/releases/.  You must have a username and password to SPN in order to access this portion of site.  Without SPN credentials, you may still download the installer and get the latest version of Elixys.

Assuming you are on a Windows OS
1. http://sofienetwork.com/github/latests_installer_exe?os=windows
2. Once downloaded, open the exe.
3. From the toolbar select Elixys->Get Latest
4. Close the installer
5. Connect to the Elixys WIFI
6. Re-Open the installer
7. Wait for Installer to connect to your Elixys.  See the Tower PC Icon
8. Once connected, select Upload
9. Select elixys.zip
10. Confirm upload version
11. Once completed, restart the control box
12. Validate the new version of Elixys is running


#### Deployment SOP
To make a version available for download on SPN
1. git checkout branch_to_deploy
2. git pull
3. git checkout master
5. git merge branch_to_deploy
6. re-run all tests
7. ./osx_installer.sh [run from the target controlbox]
8. Draft a new release https://github.com/SofieBiosciences/Elixys/releases/new
    1. Tag Version: vx.y.z @ target: master
    2. Release Version: pyelixys_vx.y.z
    3. Copy src/pyelixys_config.txt Change_Logs section into this section
    4. Drag & Drop this zip file created from ./osx_installer.sh into the binary section [Should look like linux_pyelixys_vx.y.z.zip]
    5. Publish Release
    6. Validate https://www.sofienetwork.com/github/releases/ displays the option for your new version.  Validate selecting that version prompts a selection of LINUX

### Categorizing Issues & Ticket Types

#### Python
Python is the center-point of Elixys.  It controls how each sequence operation functions [timing, turning on/off valves, record creation],and it is the layer that does all communication between the User Interface and the Firmware.  If a code-change is around a business rule; think this is the layer that will need to change.

Pyelixs changes will be written in a TDD format [Test Driven Development].
This means, prior to source code being developed; a test must be written to validate it is working against the simulator.  This means, immediatly after writing the test, we would expect failure.  Develop the source code afterwards to make a passing test.  For more details on developing Pyelixys tests visit the [README](https://github.com/SofieBiosciences/Elixys/blob/master/src/test/README.md)


#### C++
C++ contains all the low-level controls for the hardware.  This layer should very seldomly be changed once hardware revisions has been finalized.

#### Javascript
Javascript contains the workflow of the User Interface.  This contains rules such as, what the user will be able to control and what will be displayed next to the user.

#### CSS/SCSS HTML
CSS/SCSS and HTML is used to visually display the controls and data to the user.


### Tracking Deployed Software Revision Changes/History


## Intro to Software Version Naming Standards
[Version Naming](./Versions/version_naming.md)


