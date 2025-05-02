# <h1> Creating a Windows Answer File for Automated Installation and Deployment on Windows Server 2022 </h1>


<h3> Setting up the environment</h3>


Due to the nature of the lab being set in a simulated air-gapped system, the files were provided within a folder within the lab but in general, to start off the process of the setting up the development environment, the following files will be needed:
  

<ul>
  <li>Windows Assessment and Deployment Kit (ADK) </li>
  <li>Preinstallation Environment Add-ons for the (ADK PE)</li>
  <li>Microsoft Deployment Toolkit (MDT)</li>
</ul>

<hr>
<ol>
  <li>Starting with the Microsoft Deployment Toolkit, run the installer entitled "adksetup.exe" </li>
<br>
  <li>Accept the defaults of the Windows Kits Privacy screen and click next, doing the same until you reach the "Select the features you want to install" screen.</li>
</ol>
<br>
❗ <b>If you have features that are specific to your organizations implementation process be sure to configure them here</b> ❗

<br>
<br> 

[![Select Features Screen](https://pluralsight2.imgix.net/labs/assets/38a13cb1-25ef-46b7-8010-3ac059032c36_ADK%20Select%20the%20features%20you%20want%20to%20install.jpg)](https://pluralsight2.imgix.net/labs/assets/38a13cb1-25ef-46b7-8010-3ac059032c36_ADK%20Select%20the%20features%20you%20want%20to%20install.jpg)


