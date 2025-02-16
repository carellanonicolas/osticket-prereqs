<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

## Overview
This repository provides a structured approach to setting up osTicket on a Windows 10 Virtual Machine hosted in Microsoft Azure.

## Prerequisites
Ensure the following are available before installation:
- Azure Virtual Machine (Windows 10, 4 vCPUs)
- Remote Desktop Access
- Internet Information Services (IIS) with CGI enabled
- PHP 7.3.8, MySQL 5.5.62, and required modules
- osTicket v1.15.8 installation files

## Installation Steps
1. **Create an Azure Virtual Machine:**
   - Sign in to the [Azure Portal](https://portal.azure.com/)
   - Click **Create a resource** → **Virtual Machine**
   - Choose the following configuration:
     - **Operating System:** Windows 10 (latest available version)
     - **Size:** Standard_D4s_v3 (4 vCPUs)
     - **Username:** (Set to whatever you'll remember)
     - **Password:** (Set to whatever you'll remember)
   - Click **Review + Create**, then **Create**
     
<p>
<img <img width="1440" alt="os ticket STEP 1" src="https://github.com/user-attachments/assets/7a12bd3b-7d05-4284-b462-9b878b02b825"/>
<img /> 
</p>

2. **Enable IIS with CGI:**
   - Log into the VM using Remote Desktop
   - Open **Control Panel** → **Programs** → **Turn Windows features on or off**
   - Check **Internet Information Services (IIS)** and under **Application Development Features**, enable **CGI**
   - Click **OK** and restart the VM
     
<p>
<img <img width="1123" alt="OS STEP 4" src="https://github.com/user-attachments/assets/0858edd1-426b-4bd5-a87d-3f7670d8668d" />
<img /> 
<img width="1440" alt="OS STEP 5" src="https://github.com/user-attachments/assets/3927c2e5-786a-492b-a6d8-55307b1700e4" />
<img /> 
</p>

3. **Install PHP, MySQL, and osTicket:**
   - Download and extract [osTicket-Installation-Files.zip](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)
   - Install PHP 7.3.8 and configure IIS to use it
   - Install MySQL 5.5.62 and configure the database
   - Copy the `upload` folder to `C:\inetpub\wwwroot\osTicket`

#### Additional Configuration Steps
1. **Install and Configure PHP:**
   - Install **PHP Manager for IIS** from the `osTicket-Installation-Files` folder.
   - Install the **Rewrite Module**.
   - Create the directory `C:\PHP`.
   - Extract `php-7.3.8-nts-Win32-VC15-x86.zip` into `C:\PHP`.
   - Install `VC_redist.x86.exe`.

2. **Install and Configure MySQL:**
   - Run `mysql-5.5.62-win32.msi`.
   - Select **Typical Setup** → Install.
   - Launch the Configuration Wizard:
     - **Standard Configuration**
     - Set **root** username and password.
     - Click **Execute** to complete the setup.

3. **Configure IIS for PHP:**
   - Open IIS Manager as an Administrator.
   - Register PHP in IIS (`C:\PHP\php-cgi.exe`).
   - Restart IIS.

4. **Deploy osTicket:**
   - Extract `osTicket-v1.15.8.zip`.
   - Copy the `upload` folder to `C:\inetpub\wwwroot`.
   - Rename `upload` to `osTicket`.
   - Restart IIS and navigate to `http://localhost/osTicket`.

5. **Enable Required PHP Extensions:**
   - In IIS, open **PHP Manager** → Enable the following:
     - `php_imap.dll`
     - `php_intl.dll`
     - `php_opcache.dll`
   - Refresh the osTicket site in your browser and verify changes.

4. **Set Permissions:**
   - Assign Permissions: ost-config.php
   - Disable inheritance -> Remove All
   - New Permissions -> Everyone -> All

     **Note:** Disabling inheritance and granting full permissions to `Everyone` is **not** best practice in a real-world scenario. This is done here only for demonstration purposes and should be restricted properly in a production environment.


5. **Start osTicket Configuration:**
   - Open a browser and go to `http://localhost/osTicket`
   - Follow the setup wizard to complete the installation

## Notes
After installation, delete the `setup` directory and restrict permissions for `ost-config.php` as per security best practices.


