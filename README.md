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

- In Azure Settings make Client-1 DNS seeting to DC-1 Private IP Address
    - Virtual machines > DC-1 > Network settings > (Click the NIC primary) > DNS servers > (Change to custom) > Enter the private IP of DC-1
      
      ![image](https://github.com/user-attachments/assets/79faf215-daa1-4327-9acd-0b429665ce14)
    
- Login to Client-1 via Remote Desktop and ping DC-1 test the connectivity and check the DNS to it set to DC-1 private IP
  ![image](https://github.com/user-attachments/assets/f5b90a52-ac0b-40ea-bff3-b168d3cea45a)



      

