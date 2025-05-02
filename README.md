# Windows Server 2022 — Rapid‑Prep Deployment Toolkit  
*Derived from the Pluralsight “Prepare Your Deployment Environment” lab materials*

---

## 1 Tooling Checklist

Inside the **Lab Files** folder on the VM desktop you will find every installer required for the exercise.  
Copy the same three toolkits if you are repeating these steps in a corporate network:

1. **Windows Assessment and Deployment Kit (ADK)**  
2. **Windows PE add‑ons for ADK**  
3. **Microsoft Deployment Toolkit (MDT)**  

> **Why these three?**  
> *ADK* supplies Windows System Image Manager for answer‑file creation, *WinPE* gives you a lightweight boot OS, and *MDT* glues the workflow together with Deployment Workbench.

---

## 2 Install Windows ADK

1. Mount `…_ADK.iso` (double‑click).  
2. Run **`adksetup.exe`**.  
3. Accept default location ➔ **Next**.  
4. Keep Windows Kits privacy defaults ➔ **Next**.  
5. Read the EULA and hit **Accept**.  
6. Leave the feature list untouched unless your organization has a hardened baseline ➔ **Install**.  

![ADK feature selection](https://pluralsight2.imgix.net/labs/assets/38a13cb1-25ef-46b7-8010-3ac059032c36_ADK%20Select%20the%20features%20you%20want%20to%20install.jpg)

7. Approve the UAC prompt.

![UAC prompt](https://pluralsight2.imgix.net/labs/assets/2c1e5e18-3783-46e0-bbe7-250c23d0533b_UACPrompt.jpg)

8. Two minutes later you should see the completion dialog; click **Close**.

![ADK install complete](https://pluralsight2.imgix.net/labs/assets/f5c8d207-d748-4073-9d33-0bc0aa9f744f_ADKInstallComplete.jpg)

9. Right‑click the mounted drive ➔ **Eject**.

![Eject ISO](https://pluralsight2.imgix.net/labs/assets/2d87050d-0e14-4a4a-89c8-51de7eb28f72_Eject.png)

---

## 3 Add Windows PE Components

1. Mount `…_ADKWINPEADDONS.iso`.  
2. Launch **`adkwinpesetup.exe`**.  
3. Click through default location ➔ privacy ➔ license screens.  
4. On **Select the features you want to install**, leave everything selected ➔ **Install**.

![WinPE feature selection](https://pluralsight2.imgix.net/labs/assets/1c25a9ae-0a81-4c03-86ee-6c6253162aab_ADKPE%20Select%20the%20features%20you%20want%20to%20install.jpg)

5. Approve UAC; in roughly three minutes the WinPE add‑ons finish.

![WinPE install complete](https://pluralsight2.imgix.net/labs/assets/78fd12d1-f779-44cd-a363-0121be3ae5e6_ADKPEInstallComplete.jpg)

6. Close the wizard and eject the ISO as before.

---

## 4 Install Microsoft Deployment Toolkit

1. In **Lab Files**, run **`MicrosoftDeploymentToolkit_x64.exe`**.  
2. **Next** ➔ accept the license ➔ **Next** twice.  
3. Hit **Install**; MDT takes under 30 seconds.  
4. Click **Finish**.

MDT’s **Deployment Workbench** and ADK’s **Windows SIM** are now available for the remaining lab challenges (answer‑file creation, image capture, and deployment).

---

## 5 Next Steps

- Use *Windows SIM* to craft an unattended XML for Windows Server 2022.  
- Import the OS, drivers, and answer file into *Deployment Workbench*.  
- Test a fully automated deployment inside your sandbox or pilot network.

> **Note:** In production, these setup tasks would normally be scripted or folded into a formal build pipeline—still, the manual run‑through makes a great “proof‑of‑understanding” artifact for your GitHub portfolio.

---

## 1 Kick‑off: Open Deployment Workbench

1. Click **Start** and type **Deployment Workbench**.  
2. When prompted by UAC, choose **Yes**.

![Launch Deployment Workbench](https://pluralsight2.imgix.net/labs/assets/6b05d354-11ae-45a6-852b-a51623722429_MDTStartDeploymentWorkbench.jpg)

---

## 2 Create Your Deployment Share

1. In the MMC, right‑click **Deployment Shares** ➔ **New Deployment Share**.  
2. **Path** – accept `C:\DeploymentShare` ➔ **Next**.  
3. **Share name** – leave `DeploymentShare$` ➔ **Next**.  
4. **Descriptive name** – keep **MDT Deployment Share** ➔ **Next**.  
5. **Options** – stick with defaults (screenshot below) ➔ **Next**.

![Default share options](https://pluralsight2.imgix.net/labs/assets/555214fb-7c74-43e1-92d8-afa289a8e4c1_MDTNewDeploymentShareOptions.jpg)

6. Review the **Summary**, then click **Next**. ≈10 seconds later you should see **Confirmation**.

![Deployment share created](https://pluralsight2.imgix.net/labs/assets/30883f5b-c07c-4b59-b813-73a66aa5826b_MDTNewDeploymentShareConfirmation.jpg)

7. Hit **Finish**.

---

## 3 Import Windows Server 2022

1. From **Lab Files**, double‑click `SERVER_EVAL_x64FRE_en-us.iso`; Windows mounts it.

![Mounted ISO](https://pluralsight2.imgix.net/labs/assets/5e1b25ba-29b2-4067-b394-30a687117257_MountedWS2022ISO.jpg)

2. In Deployment Workbench, expand your share ➔ right‑click **Operating Systems** ➔ **Import Operating System**.  
3. Choose **Full set of source files** ➔ **Next**.  
4. **Browse** to your mounted DVD drive (`D:`) and click **OK**.

![Select DVD source](https://pluralsight2.imgix.net/labs/assets/4c4b1b96-7681-4bd9-85aa-9f386120da05_Screenshot%202024-12-09%20at%2011.54.37%E2%80%AFAM.png)

5. Accept the default destination folder name ➔ **Next** ➔ **Next** again.  
6. After < 1 minute the wizard completes.

![Import finished](https://pluralsight2.imgix.net/labs/assets/8364c17e-1520-4737-8fd4-ec5f6ba97400_MDTImportOperatingSystemComplete.jpg)

7. Click **Finish** and confirm the OS list appears.

![OS list view](https://pluralsight2.imgix.net/labs/assets/c4600fa3-5e08-4a65-bd90-5b0b191803aa_MDTImportOperatingSystemCompleteShowOSs.jpg)

---

## 4 Create a Task Sequence

1. Right‑click **Task Sequences** ➔ **New Task Sequence**.  
2. **General Settings** – ID: **DepWS2022**, Name: **Deploy Windows Server 2022**.

![General settings](https://pluralsight2.imgix.net/labs/assets/59a48f48-1556-46fb-a91e-8ab5d418f5ce_MDTNewTaskSequenceGeneralSettings.jpg)

3. **Template** – choose **Standard Server Task Sequence** ➔ **Next**.  
4. **Select OS** – pick **Windows Server 2022 SERVERDATACENTER** ➔ **Next**.  
5. Leave product‑key, organization, and admin‑password pages at defaults ➔ **Next** through **Summary**, then **Finish**.

---

## 5 Update the Deployment Share

1. Right‑click your share ➔ **Update Deployment Share**.  
2. Accept default **Options** ➔ **Next** ➔ **Next** to build.≈6 minutes later:

![Update complete](https://pluralsight2.imgix.net/labs/assets/18d7d2be-8c9d-4aab-837b-82bd9232cd4d_UpdateDeploymentShareComplete.jpg)

3. Click **Finish**.

> **Result:** MDT has generated a custom boot ISO **and** the initial Windows Answer File, ready for further editing in the next challenge.

Keep Deployment Workbench open—you’ll tweak that answer file shortly. Great progress; fire up the next lab step, then grab a well‑earned coffee while the 15‑minute process runs!

# Tailoring Your Windows Server 2022 Answer File with Windows SIM  
*Synthesized from the Pluralsight “Customize the Windows Answer File” lab*

---

## 1 Shortcut: Crack Open *Unattend.xml*

1. In **Deployment Workbench** expand **Task Sequences**, right‑click **Deploy Windows Server 2022** ➔ **Properties**.  
2. On **OS Info** choose **Edit Unattend.xml**.

![Edit Unattend](https://pluralsight2.imgix.net/labs/assets/94f20308-2263-44d2-8279-ab27f7e24a05_MDTTaskSequenceEditUnattendXML.jpg)

3. When the catalog‑generation PowerShell kicks off, click **Stop Execution** to skip the 15‑minute build (lab‑only time‑saver).

![Stop execution](https://pluralsight2.imgix.net/labs/assets/1aeb1ee6-ee33-477a-97b6-154c356dc9cd_MDTTaskSequenceStopExecution.jpg)

4. Wait for the “Unable to edit” pop‑up, click **OK**, then hit **Edit Unattend.xml** once more.

![Error message (expected)](https://pluralsight2.imgix.net/labs/assets/ecdebf2b-0cb8-4a1a-8982-59a374c20c27_MDTTaskSequenceStopExecutionErrorMessage.jpg)

   *Result:* **Windows System Image Manager** (WSIM) springs to life with your answer file loaded.

![WSIM initial view](https://pluralsight2.imgix.net/labs/assets/f006ae0d-cdbd-40b2-89a6-2df240060998_WSIMInitialLaunch.jpg)

---

## 2 Add a Product Key (Pass 1 windowsPE)

1. In the **Windows Image** pane:  
   `Components` ➔ **amd64_Microsoft‑Windows‑Setup…** ➔ right‑click **UserData** ➔ **Add Setting to Pass 1 windowsPE**.

![Add ProductKey node](https://pluralsight2.imgix.net/labs/assets/711d4f74-0975-46e3-b561-a6ad80f12381_WSIMAddProductKeyToPass1.jpg)

2. In the **Answer File** pane select **ProductKey**, then on the **Properties** panel set **Key** to **made‑up**.

![Enter key](https://pluralsight2.imgix.net/labs/assets/06e3a556-a4d2-4cb1-8cf6-eaf551bd90f0_Screenshot%202024-12-09%20at%2012.41.13%E2%80%AFPM.png)

---

## 3 Embed Support Info (Pass 4 specialize)

1. Still in **Windows Image**:  
   `Components` ➔ **amd64_Microsoft‑Windows‑Shell‑Setup…** ➔ right‑click **OEMInformation** ➔ **Add Setting to Pass 4 specialize**.

![Add OEMInformation](https://pluralsight2.imgix.net/labs/assets/1e595ca3-48a6-4b98-b4ec-ffccebb1a931_WSIMAddOEMInformationToPass4.jpg)

2. Populate the fields:

   | Field | Value |
   |-------|-------|
   | Manufacturer | Pluralsight |
   | Model | Learner VM |
   | SupportHours | 24/7 |
   | SupportPhone | 1‑801‑784‑9007 |
   | SupportURL | https://help.pluralsight.com/help |

![OEMInformation values](https://pluralsight2.imgix.net/labs/assets/abc82ad6-2530-4ff3-a7e9-5e491ae27dd7_WSIMAddOEMInformationAdd.jpg)

---

## 4 Configure Accounts (Pass 7 oobeSystem)

### 4.1 Administrator Password

1. In **Windows Image** locate **UserAccounts** (same Shell‑Setup component) ➔ **Add Setting to Pass 7 oobeSystem**.

![Add UserAccounts](https://pluralsight2.imgix.net/labs/assets/8d4cc7f1-f808-45aa-8579-d58d034f97c0_WSIMAddUserAccountsToPass7.jpg)

2. In **Answer File** open **UserAccounts** ➔ select **AdministratorPassword** ➔ set **Value** to **$up3r$3cretP@$$w0rd**.

![Set admin password](https://pluralsight2.imgix.net/labs/assets/f42c935e-7530-434d-b71e-a53b74770f94_WSIMAddUserAccountsSetLocalAdminPassword.jpg)

### 4.2 Create a Local User

1. Right‑click **LocalAccounts** ➔ **Insert New LocalAccount**.

![Insert LocalAccount](https://pluralsight2.imgix.net/labs/assets/f8b760b0-53af-47b6-b202-82704d4f1706_WSIMAddUserAccountsAddLocalAccount.jpg)

2. Fill in the new account’s properties:

   | Property | Value |
   |----------|-------|
   | Description | A local user account |
   | DisplayName | Local User |
   | Group | Users |
   | Name | LocalUser |

![LocalAccount values](https://pluralsight2.imgix.net/labs/assets/52bfb018-5f41-4187-b06a-fbbedf334e8b_WSIMAddUserAccountsAddLocalAccountAdd.jpg)

3. Expand **LocalAccount\[Name="LocalUser"]** ➔ select **Password** ➔ set **Value** to **3v3nm0re$up3r$3cretP@$$w0rd**.

![Set local‑user password](https://pluralsight2.imgix.net/labs/assets/bf8d2888-0635-4a4d-81ed-308f58c9ebcf_WSIMAddUserAccountsAddLocalAccountSetPassword.jpg)

---

## 5 Save & Keep WSIM Open

You’ll validate the file in the next lab step, so **leave WSIM running**.  
Passwords are stored in encoded form—be sure to keep them in a secure vault for production!

*Great job—your answer file now carries a product key, OEM metadata, an admin password, and a pre‑created local user. Time to move on to validation and final save.*





****
# Validate & Save Your Customized *Unattend.xml*  
*Adapted from the Pluralsight “Validate the Windows Answer File” lab*

---

## 1 Run Validation in Windows SIM

1. In **Windows System Image Manager** (WSIM) click the **Validate Answer File** icon on the toolbar.

![Validate button](https://pluralsight2.imgix.net/labs/assets/801b07c5-ae79-4b7b-919d-95e79980dc79_WSITValidateAnswerFileButton.jpg)

2. Within seconds WSIM populates the **Messages** pane with warnings, errors, or informational notes.

![Messages pane](https://pluralsight2.imgix.net/labs/assets/9860312e-c51f-4f9b-8ffc-cad0e6891be2_WSIMMessagesPane.jpg)

> **Tip:** Double‑click any message to jump directly to the related node in the Answer File tree.

---

## 2 Clean Up an Unused Setting

1. Locate the warning *“This setting has not been modified. It will not be saved to the answer file.”*  
2. Double‑click it—WSIM highlights the unused **DomainAccounts** element.  
3. Right‑click the highlighted node ➔ **Delete**.

![Delete unused element](https://pluralsight2.imgix.net/labs/assets/4287ead1-e1c8-47ae-8a29-5a7334174a59_WSITValidateAnswerFileDeleteUnused.jpg)

4. Run **Validate Answer File** again; the warning disappears.

![Clean validation list](https://pluralsight2.imgix.net/labs/assets/b85c8d85-d40d-43ce-b998-87bc0369164a_WSITValidateAnswerFileDeleteUnusedResolved.jpg)

> In production you’d research each message, but for lab speed you may ignore obsolete or informational entries once you understand their impact.

---

## 3 Save the Answer File

1. Click the **Save** icon (or press *Ctrl+S*).

![Save button](https://pluralsight2.imgix.net/labs/assets/3611f13f-efa7-4e24-818f-157b6a9e94ae_WSIMSaveButton.jpg)

2. If your workflow requires version control elsewhere, choose **File ➔ Save Answer File as…** and commit it to your repo.

![Save As option](https://pluralsight2.imgix.net/labs/assets/f9da5e1c-a666-41e9-a637-5af239503e73_WSIMSaveAs.jpg)

3. WSIM warns about remaining validation notes—click **Yes** to proceed (lab‑safe).

---

## 4 Next Steps

- Mount the new ISO generated by MDT and test an unattended deployment.  
- Iterate: adjust → validate → save until validation is clean and deployment passes internal QA.

*You’ve now completed the full lifecycle—creation, customization, validation, and preservation—of a Windows Server 2022 answer file. Great work!*
