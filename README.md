<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

---

### **1. Download File**
- **Windows**: Windows 10, Windows Server 2012 or newer.
- **Linux**: Ubuntu, CentOS, or other Linux distributions with web server support.

---

### **2. Web Server**
- **IIS (Internet Information Services)**: Version 7 or newer for Windows.
- **Apache**: For Linux or macOS setups.

---

### **3. PHP**
- **Supported PHP Versions**: 7.2 to 7.4 (osTicket does not support PHP 8.x as of now).
- **PHP Extensions** (these must be enabled):
  - **php_imap.dll**: For email fetching.
  - **php_intl.dll**: For internationalization support.
  - **php_opcache.dll**: For performance optimization.

---

### **4. Database**
- **MySQL 5.5 or newer** (MariaDB can also work).

---

### **5. Required Dependencies and Tools**
- **PHP Manager for IIS**: For configuring PHP with IIS (if using Windows IIS).
- **Microsoft Visual C++ Redistributable**: Required for running PHP.
- **URL Rewrite Module** (if using IIS): For clean, SEO-friendly URLs.
- **HeidiSQL** (optional): A GUI tool for managing MySQL databases.

---

### **6. Browser Access**
- A modern web browser (e.g., Chrome, Firefox, Edge) to access and configure osTicket via its web interface.

---

### **7. Hardware Requirements**
- **Processor**: Minimum 2 GHz (recommendation: multi-core).
- **RAM**: 2 GB minimum (4 GB or more recommended for larger environments).
- **Storage**: At least 10 GB free space for the operating system, database, and attachments.

---

### **8. Downloadable Files**
- **osTicket Installation Files**:
  - The main osTicket zip package (e.g., `osTicket-v1.15.x.zip`).
  - Additional dependencies (e.g., PHP, MySQL installers).

---

<h2>Installation Steps</h2>

Here’s a simple, step-by-step explanation of how to create an osTicket setup. I'll explain it in a straightforward way so it's easy to follow. Let’s break this into clear tasks:

---

### **1. Set Up the Virtual Machine in Azure**
1. **Create a VM in Azure**:
   - Go to Azure, create a **Windows 10** virtual machine with:
     - Name: **osticket-vm**
     - Size: **4 vCPUs** (this is like the computer’s brain capacity).
     - Username: **labuser**
     - Password: **osTicketPassword1!**
   - Finish creating the VM.

2. **Connect to the VM**:
   - Download the **Remote Desktop (RDP)** file from Azure.
   - Open it, log in using:
     - Username: **labuser**
     - Password: **osTicketPassword1!**

<p>
<img src="https://i.imgur.com/OPoPUs5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

---

### **2. Prepare the Files**
1. **Download the Setup Files**:
   - Inside the VM, download the `osTicket-Installation-Files.zip`.
   - Extract (unzip) it to your Desktop. Name the folder **osTicket-Installation-Files**.

</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/c6d44dc6-bfc2-4d1f-a95f-29abfd430ff9)

</p>
<p>
  
---


### **3. Set Up Windows Features**
1. **Enable IIS (Internet Information Services)**:
   - Open **Control Panel** > **Programs** > **Turn Windows features on or off**.
   - Find **Internet Information Services** (IIS).
  
  ![Screenshot 2024-11-22 202341](https://github.com/user-attachments/assets/2c66756c-cee1-41e9-bcfc-d3a02207cb0d)
   
   - Expand **World Wide Web Services** > **Application Development Features**.
   - Check the box for **CGI**, then click OK. This sets up the system to run websites.
</p>
<br />

![Screenshot 2024-11-22 202438](https://github.com/user-attachments/assets/942de91a-a9a7-43c8-9d5f-888d9202acd7)

<p>

---

</p>
<p>
  
### **4. Install Required Tools**
1. **Install PHP Manager**:
   - Go to the `osTicket-Installation-Files` folder.
   - Double-click `PHPManagerForIIS_V1.5.0.msi` to install.
     
![Screenshot 2024-11-22 203314](https://github.com/user-attachments/assets/4c91a25a-b991-4915-9393-aa50a39e0ff8)

2. **Install Rewrite Module**:
   - From the same folder, double-click `rewrite_amd64_en-US.msi`.
     
     ![Screenshot 2024-11-22 203355](https://github.com/user-attachments/assets/c5b309e1-34d4-4b04-9d02-bb981a212537)


3. **Set Up PHP**:
   - Create a new folder: `C:\PHP` (like making a new folder in your computer).
   - Extract (unzip) `php-7.3.8-nts-Win32-VC15-x86.zip` into `C:\PHP`.
     
     ![Screenshot 2024-11-22 203813](https://github.com/user-attachments/assets/f0624f0e-aa2e-4a7f-b5ef-4178f2e63929)


4. **Install Visual C++ Redistributable**:
   - Double-click `VC_redist.x86.exe` to install.
     
     ![Screenshot 2024-11-22 204007](https://github.com/user-attachments/assets/602807e6-38a8-410d-b3ea-8ec3d16abc22)


5. **Install MySQL**:
   - Run `mysql-5.5.62-win32.msi` to install MySQL (a tool to manage data).
   - Use the **Typical Setup** option.
   - During the setup wizard:
     - Choose **Standard Configuration**.
       
     ![Screenshot 2024-11-22 204120](https://github.com/user-attachments/assets/75875497-ada4-43c8-838a-e52ee72dd50e)

     - Set the username to **root** and the password to **root**.

       ![Screenshot 2024-11-22 204157](https://github.com/user-attachments/assets/b69510ff-68ca-4749-9cf5-9a1556ea088c)

</p>
<br />
  
---

### **5. Configure IIS**
1. **Register PHP with IIS**:
   - Open IIS (search for “IIS Manager” on the Start menu).
   - Go to **PHP Manager** and register PHP:
     - Path: `C:\PHP\php-cgi.exe`.
   - Restart IIS (click **Stop**, then **Start** the server in IIS).
![Screenshot 2024-11-22 204427](https://github.com/user-attachments/assets/c4423653-370b-497c-972e-6a5557032a1e)

---

### **6. Set Up osTicket**
1. **Install osTicket Files**:
   - Go to the `osTicket-Installation-Files` folder.
   - Unzip `osTicket-v1.15.8.zip`.
   - Copy the `upload` folder to `C:\inetpub\wwwroot`.
   - Rename the `upload` folder to **osTicket**.
     
     ![Screenshot 2024-11-22 205030](https://github.com/user-attachments/assets/57b11e12-aad9-47b7-91b7-da7165a5035b)


2. **Open osTicket in a Browser**:
   - Go back to IIS.
   - In **Sites -> Default -> osTicket**, click **Browse *:80**.
     
     ![Screenshot 2024-11-22 205409](https://github.com/user-attachments/assets/285c634a-460c-400a-aa03-7984cdf990d3)

   - This will open osTicket in your web browser. You might see a message about missing extensions (we’ll fix that).
     
     ![Screenshot 2024-11-22 205453](https://github.com/user-attachments/assets/1f5bfeae-f6b1-4004-8c76-52df436c1147)


3. **Enable PHP Extensions**:
   - In IIS, go to **PHP Manager** > **Enable or disable an extension**.
   - Enable:
     - `php_imap.dll`
     - `php_intl.dll`
     - `php_opcache.dll`.
   - Restart IIS and refresh the osTicket page.

     ![Screenshot 2024-11-22 205854](https://github.com/user-attachments/assets/38649ebe-46be-42f0-bf5f-fd76836c9f44)


4. **Rename the Config File**:
   - Rename this file:
     - From: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
     - To: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`.

       ![Screenshot 2024-11-22 210247](https://github.com/user-attachments/assets/03e5af96-9e81-443b-b1b7-8ea689d968b3)


5. **Set File Permissions**:
   - Right-click `ost-config.php` > Properties.
   - Disable inheritance, remove all permissions, and give **Everyone** full access.
![Screenshot 2024-11-22 210520](https://github.com/user-attachments/assets/312b1f9c-080b-4c02-832c-62d7c1b49d5a)
![Screenshot 2024-11-22 210436](https://github.com/user-attachments/assets/70ba680c-e914-41c9-b25d-c2ae9ead067d)

---

### **7. Complete Installation**
1. **Set Up osTicket in the Browser**:
   - Open the browser where osTicket is running.
   - Fill in:
     - Helpdesk Name: (e.g., **My Helpdesk**)
     - Default email: (your choice).
   - Click Continue.

2. **Create a Database**:
   - Install **HeidiSQL** from `osTicket-Installation-Files`.
   - Open HeidiSQL and connect with:
     - Username: **root**
     - Password: **root**.
    ![Screenshot 2024-11-22 211406](https://github.com/user-attachments/assets/c927dc7f-93ef-40c9-80d7-e7d60cde161c)

   - Create a database named **osTicket**.
    
![Screenshot 2024-11-22 212038](https://github.com/user-attachments/assets/d4b8b75e-0254-4dcb-8a17-8ee5c0d5925f)


3. **Finish osTicket Setup**:
   - Go back to the browser and enter:
     - Database Name: `osTicket`
     - MySQL Username: `root`
     - MySQL Password: `root`.
    ![Screenshot 2024-11-22 212154](https://github.com/user-attachments/assets/0f65cb79-699f-481a-8bb1-643901f6860b)

   - Click **Install Now**.

4. **Access osTicket**:
   - Staff Login: `http://localhost/osTicket/scp/login.php`.
     ![Screenshot 2024-11-22 212449](https://github.com/user-attachments/assets/3c5c16db-d197-448c-a54d-7f310165fd85)

   - End-User Portal: `http://localhost/osTicket/`.
   ![Screenshot 2024-11-22 212915](https://github.com/user-attachments/assets/796b1421-7113-456b-afb8-0fdaba182034)

---

### **8. Clean Up**
1. **Delete Setup Folder**:
   - Delete `C:\inetpub\wwwroot\osTicket\setup`.

2. **Change Config File Permissions**:
   - Set `C:\inetpub\wwwroot\osTicket\include\ost-config.php` to **Read-only**.

---

![Screenshot 2024-11-22 212227](https://github.com/user-attachments/assets/15450526-81e4-4d9b-8075-03b2b9e235a5)

And that’s it! You now have osTicket running and ready to use. 🎉
</p>
<p>
