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
- Make the NIC of DC-1 static
  - Virtual machines > DC-1 > Network settings > (Click the NIC primary) > IP configurations > ipconfig1 > static
        ![image](https://github.com/user-attachments/assets/bca0b490-fec8-4734-bd26-fed08e342db0)

- Create a Virtual Machine for the Client name Client 1 (Store it in the same RG)
  -   Select the OS to be Windows 10
- Now you have 2 Virtual Machines to be used and set up

   ![image](https://github.com/user-attachments/assets/ffe5d169-9d24-4976-a425-7f569de3ddda)

- Log into  DC-1 via Remote Desktop and disable all firewalls

    ![image](https://github.com/user-attachments/assets/1b4547c9-589c-49c8-8c20-556130ca3bfa)


