# osticket-prereqs
<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Setup Requirements and Installation Guide</h1>
This guide offers detailed instructions covering the requirements and setup procedure for osTicket, an open-source ticketing system for help desks. The initial step involves setting up a Virtual Machine (VM) through the Microsoft Azure Portal. Following that, we'll connect to the newly established VM using Remote Desktop Connection. It's important to know that Mac users must install Microsoft Remote Desktop beforehand. To make the setup easier, all required osTicket installation files have been bundled. <br />

<h2>Utilized Environments and Technologies</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating System Environment </h2>

- Windows 10</b> (21H2)

<h2>Prerequisite Checklist</h2>

- Microsoft Azure Virtual Machine
- [osTicket Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)
- [Remote Desktop](https://apps.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12)


<h2>Setup Procedure</h2>

<p>
<img src="https://i.imgur.com/P90vtKL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Initially, we need to install and activate Internet Information Services (IIS) within Windows. We also need to activate CGI and the Common HTTP Features. Follow the instructions outlined below:

   - Access the Control Panel on your Windows machine.
   - Select "Programs and Features."
   - Find and choose "Turn Windows features on or off."
   - In the window that opens displaying features, scroll to locate "Internet Information Services (IIS)." Tick the checkbox beside it to activate IIS.
   - Expand the "Internet Information Services (IIS)" entry.
   - Expand "World Wide Web Services."
   - Expand "Application Development Features."
   - Activate CGI by ticking its corresponding checkbox.
   - Additionally, verify that all items under "Common HTTP Features" are also activated.

Completing these actions will successfully install and activate IIS on Windows, along with CGI and the required Common HTTP Features components.
</p>
<br />

<p>
<img src="https://i.imgur.com/UofjXtm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To continue with the subsequent steps, adhere to these guidelines:

  Go to the directory containing the provided installation files.
    It's suggested to download all files together as a single zip archive for convenience. You can do this by right-clicking the installation 
  files (found near "Shared with me") and choosing "Download."
    After the zip archive is downloaded, unpack its contents into a chosen folder on your computer.

Next, we will install the PHP Manager for IIS and the Rewrite Module:

   - Find the installer for PHP Manager for IIS among the downloaded files.
   - Initiate the installation by double-clicking the installer.
   - Adhere to the prompts displayed on the screen to finish installing PHP Manager for IIS.
   - Perform the same installation procedure for the Rewrite Module.

</p>
<br />

<p>
<img src="https://i.imgur.com/OQGGXyR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

   - Make a new folder on the C:\ drive by right-clicking an empty area and choosing "New" -> "Folder." Name this folder "PHP".

   - Now, return to the location where you downloaded the files and find the PHP 7.3.8 files.

   - Choose all files and folders within the PHP 7.3.8 folder and transfer them to the newly created "PHP" folder on the C:\ drive.

   - Once the files are moved, locate the "VC_redist.x86.exe" file and begin its installation by double-clicking it. Follow the displayed prompts to finish the installation.
   - Then, find the downloaded MySQL 5.5.62 files. Launch the installer to begin the setup process.

   - While installing MySQL 5.5.62, select the "Typical Setup" choice.

   - Within the Configuration Wizard, opt for "Standard Configuration."

   - Set up a password for the MySQL database. As this is for a lab setup, a simple password like "Password1" can be used.
</p>
<br />

<p>
<img src="https://i.imgur.com/wWAeIpM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To carry on with the final setup stages, please adhere to the directions below:

1. Launch IIS (Internet Information Services) Manager with administrative privileges. You can achieve this by searching "IIS" in the Windows Start menu, then right-clicking "Internet Information Services (IIS) Manager," and choosing "Run as administrator."

2. Configure PHP within IIS:
   - Inside IIS Manager, click on the server name in the left-side navigation area.
   - Double-click "Handler Mappings."
   - From the Actions panel on the right side, select "Add Module Mapping."
   - Enter the details below in the dialog:
     - Request Path: *.php
     - Module: FastCgiModule
     - Executable: C:\PHP\php-cgi.exe (Adjust path if your PHP installation differs)
     - Name: PHP_via_FastCGI
   - Press "OK" to confirm the module mapping.

3. Restart IIS:
   - Launch IIS Manager.
   - Halt the server using the "Stop" button in the Actions panel on the right.
   - Restart the server using the "Start" button in the Actions panel.

4. Set up osTicket v1.15.8:
   - Get osTicket from the provided Installation Files Folder.
   - Unpack the contents of the downloaded archive.
   - Transfer the "upload" folder into the "C:\inetpub\wwwroot" directory.
   - Inside the "C:\inetpub\wwwroot" folder, change the name of the "upload" folder to "osTicket".

5. Restart IIS:
   - Launch IIS Manager.
   - Halt the server using the "Stop" button in the Actions panel on the right.
   - Restart the server using the "Start" button in the Actions panel.

6. Navigate to sites -> Default -> osTicket:
   - Within IIS Manager, expand the server name in the left-side navigation area.
   - Expand "Sites," then select "Default Web Site."
   - Below "Default Web Site," locate and select the "osTicket" folder.
   - In the right-side panel, click "Browse *:80".

Executing these instructions will finalize the successful installation and setup of osTicket.
</p>
<br />

<p>
<img src="https://i.imgur.com/CFXDCql.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Be aware that certain extensions are initially disabled.

   Return to the IIS Manager.

   Navigate to sites -> Default -> osTicket.

   Double-click on PHP Manager.

   Within the PHP Manager interface, select "Enable or disable an extension."
   Activate the extensions listed below by ticking their respective boxes:

      - php_imap.dll
      - php_intl.dll
      - php_opcache.dll

   Select "Apply" or "OK" to confirm the modifications.
   Reload the osTicket page in your web browser to see the updates.

</p>
<br />

<p>
<img src="https://i.imgur.com/Q9vXAmf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To proceed with the osTicket configuration and carry out the required tasks, follow this procedure:

1. Change the file name:
   - Using File Explorer, go to "C:\inetpub\wwwroot\osTicket\include\".
   - Find the file named "ost-sampleconfig.php".
   - Change its name to "ost-config.php".

2. Set permissions for "ost-config.php":
   - Right-click "ost-config.php" and choose "Properties".
   - Go to the "Security" tab, select "Disable inheritance", then choose "Remove all inherited permissions from this object".
   - Press "Add" to assign new permissions.
   - In the "Select Users or Groups" dialog, enter "Everyone" and click "Check Names".
   - Select "Everyone" and click "OK".
   - Tick the "Full control" checkbox in the "Allow" column for the "Everyone" group.
   - Select "OK" to apply the modifications.

3. Resume osTicket setup via the browser:
   - Launch your web browser and navigate to the osTicket site.
   - Select "Continue" to move forward with the configuration.
   - Enter a name for your Helpdesk system.
   - Define the primary email address for receiving customer communications.

4. Get and install HeidiSQL:
   - Download HeidiSQL from the provided installation files.
   - Execute the installer and follow the prompts to finish the installation.

5. Launch HeidiSQL and set up a new session:
   - Start HeidiSQL.
   - Initiate a new session creation by clicking "New".
   - Input these settings:
     - Network type: MySQL (TCP/IP).
     - Hostname/IP: localhost.
     - User: root.
     - Password: Password1 (assuming this was set during MySQL installation).
   - Press "Save" to store the session details.

6. Establish a connection and create the database:
   - Choose the newly created session from the list.
   - Select "Open" to establish the connection.
   - After connecting, select the "SQL" tab.
   - Within the SQL input area, type the command: `CREATE DATABASE osTicket;`
   - Hit F9 or click the "Execute" icon to execute the command, which will create the database.

Completing these actions involves renaming the configuration file, setting the necessary permissions, progressing with the osTicket setup in your browser, and establishing the "osTicket" database via HeidiSQL.
</p>
<br />

<p>
<img src="https://i.imgur.com/YZ7Eea7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
    On the osTicket setup screen within your browser, input the subsequent MySQL database information:

    - MySQL Database: osTicket
    - MySQL Username: root
    - MySQL Password: Password1 (assuming this password was set during the MySQL setup)

  Select "Install Now!" to begin the installation procedure.

</p>
<br />

<p>
<img src="https://i.imgur.com/sTQEDd6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Well done! Upon finishing these steps, osTicket should be installed correctly and function without issues. The setup procedure included downloading and setting up multiple files, activating necessary system features, and preparing a database for use by the osTicket application.
</p>
<br />
