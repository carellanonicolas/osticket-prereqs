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

2. **Enable IIS with CGI:**
   - Log into the VM using Remote Desktop
   - Open **Control Panel** → **Programs** → **Turn Windows features on or off**
   - Check **Internet Information Services (IIS)** and under **Application Development Features**, enable **CGI**
   - Click **OK** and restart the VM

3. **Install PHP, MySQL, and osTicket:**
   - Download and extract `osTicket-Installation-Files.zip` from the provided repository
   - Install PHP 7.3.8 and configure IIS to use it
   - Install MySQL 5.5.62 and configure the database
   - Copy the `upload` folder to `C:\inetpub\wwwroot\osTicket`

4. **Set Permissions:**
   ```powershell
   icacls "C:\inetpub\wwwroot\osTicket\include\ost-config.php" /inheritance:r
   icacls "C:\inetpub\wwwroot\osTicket\include\ost-config.php" /grant Everyone:F
   ```

5. **Start osTicket Configuration:**
   - Open a browser and go to `http://localhost/osTicket`
   - Follow the setup wizard to complete the installation

## Notes
After installation, delete the `setup` directory and restrict permissions for `ost-config.php` as per security best practices.


