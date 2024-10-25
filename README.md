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
Screenshots coming soon!

1. Download VMware Workstation Pro for Personal Use
  - VMware Workstation Pro became free to use for personal purposes earlier in 2024 so it was a motivation for using it for this lab
  - Downloading VMware will require signing up for an account on Broadcom which is free
  - Select the latest version of VMware for Windows or Linux, whichever is for your appropriate OS (If using macOS, you can use VMware Fusion, which is also free for personal use)
  - After downloading the executable, install VMware
2. Download Windows Server 2022 ISO
  - Search for Windows Server 2022 ISO to download for a free trial
  - Remember the location of the ISO - this will be needed momentarily!
3. Create a New Virtual Machine (VM)
  - Open VMware Workstation Pro
  - When first opening VMware Workstation, it will ask for a license, but since this is for personal use, select Use VMware Workstation for Personal Use
  - In the main window, select Create a New Virtual Machine
  - Use the Typical (Recommended) configuration and click Next
  - When the wizard asks about Guest Operating System Installation, select I will install the operating system later and click Next
  - In the dropdown for Guest operating system, select Microsoft Windows, and for Version, select Windows Server 2022 then click Next
  - Set VM name and click Next
  - For Disk Capacity, set the disk size to 20 GB since that's the minimum required for Windows Server (VMware suggests 60 GB but 20 GB is fine for our purposes) and click Next
  - Click Finish to create the new VM
4. Install Windows Server on the VM
  - Right-click on the newly created VM and select Settings
  - Under the Hardware tab, select CD/DVD (SATA)
  - In the Connection box, select Use ISO image file, then click Browse
  - Navigate to the folder containing the Windows Server ISO and select the ISO file
  - Click OK, then confirm that the VM says Using file C:\\... in the main window next to CD/DVD (SATA)
  - Click Power on this virtual machine to start the VM
  - When the "Press any key to boot from CD or DVD..." message appears on your screen, quickly press any key on the keyboard to load the ISO
    - If you miss pressing a key, a timeout message will appear and the ISO will not load - in this case, right-click the VM on the left panel of the main window and select Shut Down Guest
5. Windows Server Setup
  - In the Microsoft Server Operating System Steup, set language to install and click Next
  - Click Install Now to begin the install
  - Select "Windows Server 2022 Standard Evaluation (Desktop Experience)" for the operating system to install and click Next
    - The Desktop Experience provides the Windows GUI; the other option leaves out the GUI, requiring usage of the command line interface
  - Accept the License Terms and click Next
  - Click on Custom installation
  - The drive associated with the VM should be selected automatically - verify that it has the disk size entered earlier (20 GB) when creating the VM then click Next
  - Now wait for the OS to finish installing
  - Once the OS finishes installing, set up the Administrator account with a password you will remember, then click Finish
  - Finally, login with the Administrator account
  - Note: The free trial of Windows Server 2022 is valid for 180 days - once it expires, you can always download another ISO but you will have to install everything from scratch again
6. Installing Active Directory
  - Open up Server Manager - this will normally open automatically upon logging in
  - Click Manage in the top-right and click Add Roles and Features
  - Click Next on this Before you begin screen (This can be skipped in the future by checking the check box near the bottom before clicking Next)
  - Select Role-based or feature-based installation and click Next
  - For Server Selection, there's only one server available in the server pool, so click Next
  - In Server Roles, select Active Directory Domain Services and click Next
    - The pop-up window lets us know there are other features required before installing Active Directory, so click Add Features to acknowledge this
  - In Features, Group Policy Management should already be selected because it's required for Active Directory - verify this and click Next
  - Continue clicking Next through the wizard
  - In Confirmation, the window will list all the roles and features to be installed on the selected server
  - Click Install to begin the installation - ***DO NOT*** close the install wizard window yet because there is an important step to do after installation is complete
  - Once installation is complete, under Active Directory Domain Services, click on Promote this server to a domain controller
    - Because we are doing this setup from scratch (versus this normally already set up in a business or corporate environment), we do not have a domain controller yet and must set one up now
  - In Deployment Configuration, select Add a new forest
  - Type the domain name in the text box next to Root domain name and click Next
    - Note: Since this is for practice/home lab, use a .local suffix for the domain, but there are some best practices for selecting prefixes in more professional environments
    - An error message will pop up if a suffix like .local is not added to the name
  - In the dropdown for Forest functional level, select the most recent Windows Server
  - Type in a password that you will remember for the Directory Services Restore Mode password
  - In Additional Options, the NetBIOS domain name should auto-populate the text box with the name that was entered earlier for the domain name
  - Continue clicking Next through the wizard until the Prerequisites Check
  - In Prerequisites Check, let the wizard validate and once the prerequisites are verified, click the Install button
  - Once installation is completed, the computer needs to be rebooted after installing Active Directory Domain Services
  - After restarting, upon unlocking the computer to log in, the computer will now show the domain name plus the Admin account - log in to the Admin account
  - Verify that everything has been installed - under the Windows Administrative Tools folder in the Start Menu, all the AD tools that were installed should appear there
7. Basic AD Setup with User, Group and Organizational Unit creation
  - Open Active Directory Users and Computers, either from the Start Menu earlier or from Server Manager, by going to Tool > Active Directory Users and Computers
  - Expanding the domain with the dropdown will show the built in Organization Units (OUs) that are automatically created when a new domain is created
  - To add a new OU to a domain, right-click the domain, then select New > Organization Unit
    - Give the new OU a name and click OK - the new OU should show up under the domain
  - Within an OU, other OUs can be created, such as for Computers, Users, and Servers
  - Within a company, there are separate departments, and in AD, it is possible to group users into their specific departments
  - To create a new Group in an OU, right-click the destination OU, then select New > Group
    - Give the Group a name (like IT), and for Group scope, leave it Global
  - To create a new User in an OU, right-click the destination OU, then select New > User
    - Fill in the attributes like First name, Last name, and User logon name
      - The naming convention for user logon name may depend on the company, but for practice/home lab, can do first initial and last name
      - Creating new users can be done through something like a PowerShell script that would fill in attributes automatically - especially for multiple users at once - but for this lab and for basic understanding of the user attributes, users are manually created
    - Click Next, then set a password for the user
      - Depending on company policy, may need to check or uncheck certain boxes, but a good rule of thumb for new users is to check "User must change password at next logon" to have the user create their own password for their account

### Next Steps
Potential next steps to take after setting up AD and learning these skills may include making users members of groups, creating and using a PowerShell script to create multiple new users, or creating and setting up Group Policy Objects (GPOs) to apply to computers, users, and groups
