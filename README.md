<p align="center">
  <img src="https://www.vivantio.com/wp-content/uploads/MSAD.png" alt="Project Logo" width="50%"/>
</p>

## **Environments and Technologies Used**
- Microsoft Azure
- Active Directory
- Powershell

## **Operating Systems Used**
- Windows 10

## **Objectives**
- Create a simulated Active Directory environment with a Domain Controller and computer client for which users can log into
    - Install and Configure Active Directory
    - Create users
    - Group Policy and Managing Accounts

---

## **Implementation Steps**

### **Basic Setup**
- Create a Resource Group (RG) in Azure
  
    ![image](https://github.com/user-attachments/assets/75a3f30b-47af-43bf-92e4-3bada1dcfd50)

- Create a Virtual Network (Store it in the Same RG)
  - Search Bar > Virtual Network > Create 
  
      ![image](https://github.com/user-attachments/assets/41fd7c1b-b215-4523-8acb-550f3057058f)

- Create a Virtual Machine for the Domain Controller name DC-1 (Store it in the same RG)
  - Select the OS to be Windows Server 2022
- In Azure Setting make the NIC of DC-1 static
  - Virtual machines > DC-1 > Network settings > (Click the NIC primary) > IP configurations > ipconfig1 > static
        ![image](https://github.com/user-attachments/assets/bca0b490-fec8-4734-bd26-fed08e342db0)

- Create a Virtual Machine for the Client name Client 1 (Store it in the same RG)
  -   Select the OS to be Windows 10
- Now you have 2 Virtual Machines to be used and set up

   ![image](https://github.com/user-attachments/assets/ffe5d169-9d24-4976-a425-7f569de3ddda)

- Log into DC-1 via Remote Desktop and disable all firewalls (This is done for testing connectivity)

    ![image](https://github.com/user-attachments/assets/1b4547c9-589c-49c8-8c20-556130ca3bfa)

- In Azure Settings make Client-1 DNS setting to DC-1 Private IP Address
    - Virtual machines > DC-1 > Network settings > (Click the NIC primary) > DNS servers > (Change to custom) > Enter the private IP of DC-1
      
      ![image](https://github.com/user-attachments/assets/79faf215-daa1-4327-9acd-0b429665ce14)
    
- Login to Client-1 via Remote Desktop and ping DC-1 test the connectivity and check the DNS to it set to DC-1 private IP
  ![image](https://github.com/user-attachments/assets/f5b90a52-ac0b-40ea-bff3-b168d3cea45a)

### **Deploying Active Directory**
- Log into DC-1 via Remote Desktop and open on Server Manager
![image](https://github.com/user-attachments/assets/bcd0c549-9ae0-4b80-b939-86272dbedbe0)
- Installing Active Directory
  - Add roles and features > Click Next 3 times > Server Roles > Active Directory Domain Services > Click Next 3 times > Confrimation
  ![image](https://github.com/user-attachments/assets/0fba20c1-4f4e-488c-91f8-5280b6838adb)
  - Confirmation > Check the box > Install > (Wait for it to finish Installing) > Close
  ![image](https://github.com/user-attachments/assets/95947472-bec9-42d3-8dcf-c7b1a8141848)
  ![image](https://github.com/user-attachments/assets/c59ce33a-5bc6-411a-b8ef-e63f538bc904)
- Promoting Domain Controller and forest
  - Go to the upper right-hand corner click Notifications and click the prompt "Promote this server to a domain controller". A pop-up window will be created placing you inside the Deployment Configurations tab
    ![image](https://github.com/user-attachments/assets/3b2cb818-ebf9-4f7d-baa5-6f94c1e5ba72)
  - Deployment Configurations > Add a new forest and Enter a root domain name> Next > Create a DSRM password > Next > Uncheck "Create DNS delegation" > Click Next until Prerequisites Check tab > Install
    ![image](https://github.com/user-attachments/assets/afb8bad5-826a-4938-b59b-db157cdd2770)
    ![image](https://github.com/user-attachments/assets/0bf5bbb5-c45c-4e31-a705-2d3ef8a16044)
    ![image](https://github.com/user-attachments/assets/0afb258e-8106-4b7d-b392-3720e893b740)
    ![image](https://github.com/user-attachments/assets/b8f79c02-4169-4ade-986e-e0f99779559a)
- After Installing you will be prompted that you will sign out the machine will restart
    ![image](https://github.com/user-attachments/assets/b37093ad-54ba-4512-8ae2-aa388f7d61b7)
- Creating Domain Admins and Organization
  - After restarting login back to DC-1 with the user being the format [ mydomain.com\labuser ] ("labuser" can be replaced by the username that was set in Azure)
  - After logging in open Active Directory Users and Computers (ADUC) and create three core Organizational Units (OU called "_EMPLOYEES", "_ADMINS" and "_CLIENTS"
      right click mydomain.com > New > Organizational Unit   
  - Create a new employee named "Jane Doe" (same password) with the username of "jane_admin"
   right click _ADMINS > New > User
    ![image](https://github.com/user-attachments/assets/510c7161-b2bc-4e7a-8dc0-a69f180fd946)
    ![image](https://github.com/user-attachments/assets/ac6a085c-811d-4d12-9e35-10592b20a801)
  - Add jane_admin to the "Domain Admins" Security Group
    _ADMINS > right click Jane Doe profile > Properties > Member Of > Add > type "Domain Admins" where it states "Enter object names to select" > Check Names > Ok > Apply > Ok
    ![image](https://github.com/user-attachments/assets/ea8fd2c8-1a10-4323-87bc-9737451e1807)
  - Log out / close the connection to DC-1 and log back in as "mydomain.com\jane_admin". User jane_admin will be used as an admin account from now on.\
- Joining Client-1 to your domain
  - Login to Client-1 as labuser (created originally in Azure) and join it to the domain
    login to Client-1 > go to Setting > About > Rename this PC (advanced) > Change > Domain > type mydomain.com > Ok > a window tap will pop up requiring entering an account with the authority to join the domain > type jane_admin credentials
    
    ![image](https://github.com/user-attachments/assets/55fc4ccc-4374-4f30-b83e-8690b64cdb83)
     ![image](https://github.com/user-attachments/assets/61b00d58-f7a5-4142-a93e-0d3c7e8e80eb)
  - There will be a pop-up window saying "Welcome to the [domain name] domain". Followed by another pop-up window stating the computer will restart. Click Ok for both pop-up Windows
  - Go to DC-1 and go to Active Directory Users and Computers. Go to Computers and verify that Client-1 shows up. Then click and drag Client-1 inside the _CLIENTS OU.
    ![image](https://github.com/user-attachments/assets/6846bc92-38da-4df2-ae28-fae25f584724)
    
### **Creating users**
- Login into DC-1 as jane_admin (a user created in the previous section)
- Open PowerShell_ise as an administrator and open a new file
  ![image](https://github.com/user-attachments/assets/7b97ddbc-20e0-43b5-8d5e-31dd452974b6)

- Rename the file of your choice. Eample: CreateUsers.ps1
- Go to the following page and download the script using the link
  https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1
- Paste the script inside of the file and click run.
  ![image](https://github.com/user-attachments/assets/b01af06e-9635-404f-a029-79dd87ea83dd)
- After the script has finished generating users, go to ADUC and click on the _EMPLOYEES OU and see the users generated by the script
  ![image](https://github.com/user-attachments/assets/06e12ada-9761-453b-8fa4-f46b90873802)
- Choose one user from the  _EMPLOYEES OU and use it's credentials to log in to Client-1.
    NOTE: The password is automatically set to "Password1" and the username is in the format: "mydomain.com\ {insert username}" Example if a user is babo.baba, then the username is mydomain.com\babo.baba
- After logging in with the chosen user you can the Command Prompt to verify its credentials using commands "whoami" and "ipconfig"
  ![image](https://github.com/user-attachments/assets/3025896c-7583-4319-ae9b-5e8b932adbae)

### Enabling and Unlocking Accounts and Resetting Passwords
- Configure Group Policy to Lockout the account after 5 attempts
  - Login into DC-1 and go to Group Policy Management
    ![image](https://github.com/user-attachments/assets/b0c9f2be-b1eb-42f1-9a5e-36d7bd623a39)
  - Inside the Group Policy Management
    right-click Default Domain Policy > Edit
  - A new window will pop up called Group Policy Management Editor
    click the drop-down Security Setting > Account Policies > and click Account Lockout Policy
  - Change the Account Lockout Policy to 30 minutes duration, 5 invalid logon attempts, enable administrator account lockout, and Reset account lock counter after 10 minutes
    ![image](https://github.com/user-attachments/assets/b5ccc7f4-00b6-47c1-b53d-cfc1510b216a)
- Updating group policy
  - Login to Client-1 as an administrator to force an update for the recently modified Group Policy
  - Open the command prompt and type "gpupdate /force" as shown below

    ![image](https://github.com/user-attachments/assets/ea2ab25c-8d7d-4073-a41c-47410757dafd)
- Dealing with Account Lockouts
  - Get logged into DC-1 and pick a random user that was created previously in the the _EMPOLYEES OU (boba.baba will be used for this example)
  - After selecting a user attempt to log in to Client-1 with the wrong password at least 5 times until a message that shows the account is locked out
    ![image](https://github.com/user-attachments/assets/05879928-a9b3-4f5c-a6d3-447c22856e03)
  - Now the account has been locked we must unlock and reset the password go to DC-1 and open ADUC.
  - Right-click mydomain.com > Find > type the  name of the locked account and click Find Now
  - Under Search Results, the user account will show up, double-click on the account, and once in the properties click Account
    ![image](https://github.com/user-attachments/assets/71f38af7-b7ec-4f43-9c41-8fcae838e79a)
  - check Unlock account as highlighted above and click Apply.
  - To reset the account password, while being in the Find Users, Contacts and Group tab right-click the account and click Reset Password
    ![image](https://github.com/user-attachments/assets/df6dc4e7-158b-4b64-9726-84acc8cd96ab)
  - No the account can be logged in with recently changed user credentials
    ![image](https://github.com/user-attachments/assets/55d9b69f-b6a5-4446-91fb-92c2a3b9c985)
  - One can manually disable simply using the Find Now tool again and right-click and click Disable Account. Once the account is disabled any attempt to login will result in a failure as shown below. 
    ![image](https://github.com/user-attachments/assets/25053b4d-9a65-4416-996b-4fe16f984acd)
    ![image](https://github.com/user-attachments/assets/009b8866-740a-42be-9c58-08f9bff143a4)
- Observing Logs
  - Observing logs is vital in a help desk role to ensure system accountability and identify potential risks. Event Viewer logs provide a comprehensive record of system and user activities, aiding in tracking account actions, detecting unauthorized access, and  resolving user-specific issues efficiently. In this case, we can look at the logs or actions of the account we have chosen for this lab section.
  
  - Login to Client-1 as an administrator and open Event Viewer.
  - on the top left go to the Windows Logs drop-down and right-click security > Find > type the name of the account to observe the logs
  - The screenshot below captures an Event Viewer log indicating that a login attempt failed due to the account being disabled following recent changes
   ![image](https://github.com/user-attachments/assets/9ff4eaeb-339f-41a8-83db-727342ef96f1)
  - The log below shows the time I purposely chose the wrong password to log in to the account and was met with a login error. This shows up as an "Audit Failure" back-to-back as shown below.
    ![image](https://github.com/user-attachments/assets/ebefab8a-92c2-4cfe-826b-f2d9c09fd14e)
  - Event Viewer records a vast amount of logs covering various system events, user activities, and application behaviors. What you see are just a few examples, but there can be thousands of logs generated, depending on the system's activity level and logging configuration. These logs are categorized into sections like Application, Security, and System, offering a comprehensive overview of what's happening on a machine.












  
  
    
  

    


    


 
    




      

