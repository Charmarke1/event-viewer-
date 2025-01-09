<p align="center">
<img src="https://cdn-0.askleo.com/wp-content/uploads/2016/11/ev-2048x1075.jpg?ezimgfmt=ng%3Awebp%2Fngcb1%2Frs%3Adevice%2Frscb1-1"/>
</p>

# Monitoring Activities through Event Viewer

## Overview 
 This project demonstrates how to monitor user logins and system activities within a virtual lab environment set up in Azure. The focus of this project is to track successful and failed login attempts in a domain-based environment, using native Windows tools such as **Event Viewer** and **Group Policy Management**.

**This repository provides a step-by-step guide, screenshots, and example log files to help users**:

1. Understand how to monitor login activities.
- Learn how to filter and export important event logs (like successful and failed logins).
- Set up Group Policy for auditing logon events across the network.

**The tools use in this project**:
  - **Vitual Machine** / Domain Controller / a domain.
  - **Event Viewer** for accessing security logs.
  - **Group Policy Management** for configuring audit settings.
  - **Excel** for reviewing and analyzing exported logs.

By the end of this project, users will be able to monitor login activities, track potential security issues, and maintain a secure environment in their Azure lab or similar network.


## Lab Instruction 

**Step 1: Monitoring Logs**
---
- Login on your Domain Controller, a right click on your Window key in the domain controller 
 to see **Event Viewer** then left click on it.

<img src="https://i.imgur.com/N7EKLCs.png"/>

- Now that you are on **Event Viewer** Navigate to **Windows** Logs > **Security**.

<img src="https://i.imgur.com/QM5h345.png"/>

- Expand **Window key** to see the **security key** and click on it.
  
<img src="https://i.imgur.com/SWIkpXl.png"/>

- There you are, then click on the **filter current log...** Under **Actions** for filtering **Successful** and **failed** logs. 

<img src="https://i.imgur.com/XU5faDP.png"/>

- **Erase** < All Event IDs >, for filtering Security Logs and type **4624** (Succesful login Event ID).

<img src="https://i.imgur.com/XjpQk7D.png"/>

<img src="https://i.imgur.com/ejfru1P.png"/>

- **Erase** < All Event IDs >, for filtering specific Security Logs and type **4625** (failed login Even ID).

<img src="https://i.imgur.com/utOyYoC.png"/>

<img src="https://i.imgur.com/6OGi4FH.png"/>

**Step 2: Exporting logs to a file**
---
- **Why export logs to a file ?**  if you encounter suspicious activity (e.g., multiple failed logins), you can analyze exported logs offline to identify issues without needing constant access to the server. Sharing logs with others becomes easier when they're saved in a portable format.

- You can also filter more than one Event ID at the same time for having logs in one file, by an commas you can filtre two or three different Event ID, and we gonna use this method for **export** our logs.
  
Same process for filtering multiple Event IDs, **Window > security > Action > filter current log... and type 4624,4625**

<img src="https://i.imgur.com/2teFplw.png"/>

- As you can see we have both Event ID 4624 and 4625 filtered 
  
<img src="https://i.imgur.com/4LC4auc.png"/>

- Right-click on Security, then select Save Filtered log As....

<img src="https://i.imgur.com/1sXTPYd.png"/>

- Now time to export the file in **.evtx** format, choose the emplacement and title for not losing the data and save.

<img src="https://i.imgur.com/6MkXpON.png"/>

- To export successfully click on **Display information for these languages:** and choose your Language

<img src="https://i.imgur.com/8OfGQmE.png"/>

- As you can see the file it's on the Desktop 

<img src="https://i.imgur.com/YTq35bH.png"/>

And this the end of export succesful and failed logs from **Event Viewer** to the desktop.

**Step 3: guide to set up a Group Policy to track login events in your Azure Lab**
---
**Why setting up a group policy to track login event?**  Without Group Policy, some computers might not record the logs you need (like failed, and successful logins). Group Policy ensures:

1 Consistency: All computers follow the same rule to log events.
2 Automation: You don’t have to manually enable logging on each machine.
- Login on your Domain Controller, type on the search bar in the domain controller **Group Policy Management** then double click on it.

<img src="https://i.imgur.com/HzIK4s5.png"/>

- You can see my domain name = **mydomain.com** on the Group Policy Management 

<img src="https://i.imgur.com/UoqoWLA.png"/>

- Right-click on mydomain.com > Create a GPO in this domain, and Link it here....

<img src="https://i.imgur.com/C8cnXxB.png"/>

- Name the new GPO (e.g., "Audit Login Events Policy").
- Click OK.

<img src="https://i.imgur.com/HovzoJn.png"/>

- Expand mydomain.com Key, Right-click your selected GPO **Audit Login Events Policy** and choose Edit.

<img src="https://i.imgur.com/j5yUtFC.png"/>

- The Group Policy Management Editor will open.

<img src="https://i.imgur.com/hYd0HOZ.png"/>  

-Navigate to the following path: **Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Audit Policy**

<img src="https://i.imgur.com/AMGCaLJ.png"/> 

- In the right pane, double-click **Audit logon events**.
In the dialog box:
- Check Success to log successful login attempts.
- Check Failure to log failed login attempts.
- Click OK.

<img src="https://i.imgur.com/PHtuCq1.png"/>
