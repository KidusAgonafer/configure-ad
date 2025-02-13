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
    


 
    




      

