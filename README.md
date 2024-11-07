# Active Directory Lab

## Objective

The Active Directory Lab project was done to deepen understanding of Active Directory. The primary focus was to create a virtual machine running Windows Server 2022 that would serve as a domain controller for Active Directory, providing a sandbox environment for learning Active Directory, including creating objects like Users and containers/Organizational Units (OUs). This hands-on project was designed to generate experience with using virtual machines and understanding the creation of domains and basic functions in Active Directory.

### Skills Learned

- Creation of virtual machines (VMs)
- Installation of Windows Server on a VM
- Set up Active Directory Domain Services (AD)
- Creation of Organization Units, Groups, and Users

### Tools Used

- VMware Workstation Pro for Personal Use for creating virtual machines
- Windows Server 2022 to provide a server environment for Active Directory
- Active Directory for understanding object and container creation, and how to manipulate them

## Steps

1. Download VMware Workstation Pro for Personal Use
  - VMware Workstation Pro became <a href="https://blogs.vmware.com/workstation/2024/05/vmware-workstation-pro-now-available-free-for-personal-use.html">free for personal use</a> earlier in 2024 so it was a motivation for using it for this lab - use this link to get to the download page
  - Downloading VMware will require signing up for an account on Broadcom which is free
    <p align="center">
      <img src="https://github.com/user-attachments/assets/06dd439b-37e6-4062-98ef-451b72810034">
    </p>
  - Select the latest version of VMware for Windows or Linux, whichever is for your appropriate OS (If using macOS, you can use VMware Fusion, which is also free for personal use)
    <p align="center">
      <img src="https://github.com/user-attachments/assets/05f781c3-f18a-46e7-826b-4c80e48b8f51">
    </p>
  - After downloading the executable, install VMware
2. Download Windows Server 2022 ISO
  - While installing VMware Workstation, download the ISO for <a href="https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022">Windows Server 2022</a>
  - Remember the location of the ISO - this will be needed momentarily!
3. Create a New Virtual Machine (VM)
  - Open VMware Workstation Pro
  - When first opening VMware Workstation, it will ask for a license, but since this is for personal use, select Use VMware Workstation for Personal Use
    <p align="center">
      <img src="https://github.com/user-attachments/assets/1cb36c72-773a-4a39-90c6-cb5f484d0307">
    </p>
  - In the main window, select Create a New Virtual Machine
    <p align="center">
      <img src="https://github.com/user-attachments/assets/cfd69f70-3a35-48a4-82e6-454ba89fcec6">
    </p>
  - Use the Typical (Recommended) configuration and click Next
  - When the wizard asks about Guest Operating System Installation, select I will install the operating system later and click Next
    <p align="center">
      <img src="https://github.com/user-attachments/assets/e3986c87-a056-422d-b333-a232585f7d39">
    </p>
  - In the dropdown for Guest operating system, select Microsoft Windows, and for Version, select Windows Server 2022 then click Next
    <p align="center">
      <img src="https://github.com/user-attachments/assets/79fcf75d-2d44-491f-a811-945f4b41e015">
    </p>
  - Set VM name and click Next
  - For Disk Capacity, set the disk size to 20 GB since that's the minimum required for Windows Server (VMware suggests 60 GB but 20 GB is fine for our purposes) and click Next
  - Click Finish to create the new VM
4. Install Windows Server on the VM
  - Right-click on the newly created VM and select Settings
    <p align="center">
      <img src="https://github.com/user-attachments/assets/44258e6c-35e6-4ef1-8faf-3eda7cf2d5b1">
    </p>
  - Under the Hardware tab, select CD/DVD (SATA)
  - In the Connection box, select Use ISO image file, then click Browse
  - Navigate to the folder containing the Windows Server ISO and select the ISO file
    <p align="center">
      <img src="https://github.com/user-attachments/assets/dffbd363-17ff-490a-9f3a-aa66b60bb493">
    </p>
  - Click OK, then confirm that the VM says "Using file" in the main window next to CD/DVD (SATA)
    <p align="center">
      <img src="https://github.com/user-attachments/assets/ed58fb85-2da4-4c6e-b0b8-1baa430c06f1">
    </p>
  - Click Power on this virtual machine to start the VM
  - When the "Press any key to boot from CD or DVD..." message appears on your screen, quickly press any key on the keyboard to load the ISO
    - If you miss pressing a key, a timeout message will appear and the ISO will not load - in this case, right-click the VM on the left panel of the main window and select Shut Down Guest
    <p align="center">
      <img src="https://github.com/user-attachments/assets/d34b1ffc-deb5-4350-8e29-3027478f5389">
    </p>
5. Windows Server Setup
  - In the Microsoft Server Operating System Steup, set language to install and click Next
  - Click Install Now to begin the install
  - Select "Windows Server 2022 Standard Evaluation (Desktop Experience)" for the operating system to install and click Next
    - The Desktop Experience provides the Windows GUI; the other option leaves out the GUI, requiring usage of the command line interface
    <p align="center">
      <img src="https://github.com/user-attachments/assets/3bff9aa2-05d2-4f08-9961-1d9e4a6ed750">
    </p>
  - Accept the License Terms and click Next
  - Click on Custom installation
  - The drive associated with the VM should be selected automatically - verify that it has the disk size entered earlier (20 GB) when creating the VM then click Next
  - Now wait for the OS to finish installing - the system will restart automatically
  - Once the OS finishes installing, set up the Administrator account with a password you will remember, then click Finish
  - Finally, login with the Administrator account
    <p align="center">
      <img src="https://github.com/user-attachments/assets/12265222-730c-4789-9658-0a58826a3a29">
    </p>
  - Note: The evaluation of Windows Server 2022 is valid for 180 days - once it expires, you will have to install everything from scratch again
    <p align="center">
      <img src="https://github.com/user-attachments/assets/9f2df78a-4624-4bc7-8b89-9a4b75238070">
    </p>
6. Installing Active Directory
  - Open up Server Manager - this will normally open automatically upon logging in, but if the window is closed, Server Manager can be opened from the Start Menu
    <p align="center">
      <img src="https://github.com/user-attachments/assets/6cac6a25-e531-4ace-9cee-f92c5bb43355">
    </p>
  - Click Manage in the top-right and click Add Roles and Features
    <p align="center">
      <img src="https://github.com/user-attachments/assets/c79afa05-7fc2-4173-9fe6-668abda38d4f">
    </p>
  - Click Next on this Before you begin screen (This can be skipped in the future by checking the check box near the bottom before clicking Next)
  - Select Role-based or feature-based installation and click Next
  - For Server Selection, there's only one server available in the server pool, so click Next
  - In Server Roles, select Active Directory Domain Services and click Next
    - The pop-up window lets us know there are other features required before installing Active Directory, so click Add Features to acknowledge this
    <p align="center">
      <img src="https://github.com/user-attachments/assets/d50c152a-014f-4a0a-8016-3ec5000523cb">
    </p>
  - In Features, Group Policy Management should already be selected because it's required for Active Directory - verify this and click Next
    <p align="center">
      <img src="https://github.com/user-attachments/assets/d0c7fc6b-9001-4c5a-9b83-e53e63a6b789">
    </p>
  - Continue clicking Next through the wizard
  - In Confirmation, the window will list all the roles and features to be installed on the selected server
  - Click Install to begin the installation - ***DO NOT*** close the install wizard window yet because there is an important step to do after installation is complete
  - Once installation is complete, under Active Directory Domain Services, click on Promote this server to a domain controller
    - Because we are doing this setup from scratch (versus this normally already set up in a business or corporate environment), we do not have a domain controller yet and must set one up now
    <p align="center">
      <img src="https://github.com/user-attachments/assets/c8c50a53-e11a-4105-b945-f331fd1e4069">
    </p>
  - In Deployment Configuration, select Add a new forest
  - Type the domain name in the text box next to Root domain name and click Next
    - Note: Since this is for practice/home lab, use a .local suffix for the domain, but there are some best practices for selecting prefixes in more professional environments
    - Note 2: An error message will pop up if a suffix like .local is not added to the name
    <p align="center">
      <img src="https://github.com/user-attachments/assets/75158280-e6d3-47df-9bcc-4157adf1773e">
    </p>
    <p align="center">
      <img src="https://github.com/user-attachments/assets/9e503aa6-b4d1-4338-ab73-b242a470d903">
    </p>
  - In the dropdown for Forest functional level, select the most recent Windows Server
    <p align="center">
      <img src="https://github.com/user-attachments/assets/ee908eab-cd03-4e6e-bf40-9b1af70abce4">
    </p>
  - Type in a password that you will remember for the Directory Services Restore Mode password, then click Next
  - In DNS Options, click Next
  - In Additional Options, the NetBIOS domain name should auto-populate the text box with the name that was entered earlier for the domain name
    <p align="center">
      <img src="https://github.com/user-attachments/assets/e8b0f613-dcdd-44b6-a75b-a9365c4ebcf4">
    </p>
  - Continue clicking Next through the wizard until the Prerequisites Check
  - In Prerequisites Check, let the wizard validate and once the prerequisites are verified, click the Install button
    <p align="center">
      <img src="https://github.com/user-attachments/assets/0bc19d1c-97e3-429b-9c20-5fe715c89479">
    </p>
  - Once installation is completed, the computer needs to be rebooted after installing Active Directory Domain Services
  - After restarting, upon unlocking the computer to log in, the computer will now show the domain name plus the Admin account - log in to the Admin account
    <p align="center">
      <img src="https://github.com/user-attachments/assets/1c6809ec-1e8e-4677-9743-25393a1bd15f">
    </p>
  - Verify that everything has been installed - under the Windows Administrative Tools folder in the Start Menu, all the AD tools that were installed should appear there
    <p align="center">
      <img src="https://github.com/user-attachments/assets/e86510e5-e8d7-45cb-a938-7c43e8bb9697">
    </p>
7. Basic AD Setup with User, Group and Organizational Unit creation
  - Open Active Directory Users and Computers, either from the Start Menu earlier or from Server Manager, by going to Tools > Active Directory Users and Computers
    <p align="center">
      <img src="https://github.com/user-attachments/assets/f17a6f71-1416-4044-977f-ee4d8ae45250">
    </p>
  - Expanding the domain with the dropdown will show the built in Organization Units (OUs) that are automatically created when a new domain is created
    <p align="center">
      <img src="https://github.com/user-attachments/assets/2aeb9b0f-ae30-4211-9c5a-addc5e62f4bb">
    </p>
  - To add a new OU to a domain, right-click the domain, then select New > Organization Unit
    <p align="center">
      <img src="https://github.com/user-attachments/assets/c2664f92-c96c-4aea-9445-ddc4a1a6dc75">
    </p>
  - Give the new OU a name and click OK - the new OU should show up under the domain
    <p align="center">
      <img src="https://github.com/user-attachments/assets/601af32b-011c-422b-8956-d3b7aae31086">
    </p>
  - Within an OU, other OUs can be created, such as for Computers, Users, and Servers
    <p align="center">
      <img src="https://github.com/user-attachments/assets/ba280357-408f-450e-8afc-0cae1d245927">
    </p>
  - Within a company, there are separate departments, and in AD, it is possible to group users into their specific departments
  - To create a new Group in an OU, right-click the destination OU, then select New > Group
    <p align="center">
      <img src="https://github.com/user-attachments/assets/fb876fb5-52fc-416a-902e-6b92ce9b0ed9">
    </p>
  - Give the Group a name (like IT), for Group scope, select Global, and for Group type, select Security
    <p align="center">
      <img src="https://github.com/user-attachments/assets/aa6f6e0f-516f-48bf-a80b-e9e98b0159a2">
    </p>
    <p align="center">
      <img src="https://github.com/user-attachments/assets/f8365dc1-14da-4183-819f-d0075e744177">
    </p>
  - To create a new User in an OU, right-click the destination OU, then select New > User
    <p align="center">
      <img src="https://github.com/user-attachments/assets/d5c0c350-0457-4e5e-9ff9-13ed81db0568">
    </p>
  - Fill in the attributes like First name, Last name, and User logon name - the naming convention for user logon name may depend on the company, but for practice/home lab, can do first initial and last name
    - Note: Creating new users can be done through something like a PowerShell script that would fill in attributes automatically - especially for multiple users at once - but for this lab and for basic understanding of the user attributes, users are manually created
    <p align="center">
      <img src="https://github.com/user-attachments/assets/c57f6360-3516-4a7b-876e-520f8d700423">
    </p>
  - Click Next, then set a password for the user
    - Depending on company policy, may need to check or uncheck certain boxes, but a good rule of thumb for new users in the corporate environment is to check "User must change password at next logon" to have the user create their own password for their account
    <p align="center">
      <img src="https://github.com/user-attachments/assets/d165ff22-a655-41aa-a0e4-3dbadadd5c5f">
    </p>
  - Click Finish to complete user creation and you should see the new user in the OU
    <p align="center">
      <img src="https://github.com/user-attachments/assets/e4f5d573-b443-4b84-96d1-e181f7226e82">
    </p>
    <p align="center">
      <img src="https://github.com/user-attachments/assets/4c7dabed-e52c-4439-bdd5-35254c801e6b">
    </p>
     
### Hands-On Activity

- In a company, there are more departments than just the IT department - create Groups for other departments like HR, Accounting, Sales, Management
- Add 2-3 Users into the Users OU

### Next Steps

Potential next steps to take after setting up AD and learning these skills may include making users members of groups, creating and using a PowerShell script to create multiple new users, or creating and setting up <a href="https://github.com/koliman/GPO-Lab">Group Policy Objects (GPOs)</a> to apply to computers and users
