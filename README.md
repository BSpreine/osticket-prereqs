<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
In this tutorial, we outline the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<!--- <h2>Video Demonstration</h2>(coming soon!) -->

<!--- - ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com) -->

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)

<h2>High-Level Steps</h2>

- Creating Resources (VMs)
- Installation/Enable IIS
- Install PHP Manager for IIS
- Install Rewrite Module
- Create directory C:\PHP
- Install PHP 7.3.8
- Install VC_redist.x86.exe
- Install MySQL
- Install osTicket/Enable extensions
- Intall HeidiSQL

<h2>Actions and Observations</h2>

#### Part 1 (Create our Resources)
- Create a Resource Group
- Create a Windows 10 Virtual Machine (VM)
    - While creating the VM, select the previously created Resource Group
    - While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet

<br />

#### osTicket Resource Group.
<p>
<img src="https://i.imgur.com/c7nshYx.png" height="60%" width="60%" alt="osTicket Resource Group"/>
</p>

#### osTicket VM CMD Line
<p>
<img src="https://i.imgur.com/pjijWGo.png" height="60%" width="60%" alt="osTicket VM"/>
</p>

</br>

#### Part 2 (Download and Install Files from the 'Installation Files' Folder inside of the VM)
- Install/Enable IIS in Windows with CGI
    - World Wide Web Services --> Application Development Features --> [x] CGI
    - Open new web browser and check 127.0.0.1 to ensure it was done properly.
- Install PHP Manager for IIS
- Install Rewrite Module
- Create Directory C:\PHP
- Unzip contents from PHP 7.3.8 to newly created C:\PHP (choose to keep file)

#### Installation Files.
<p>
<img src="https://i.imgur.com/Nysvo4I.png" height="50%" width="50%" alt="Installation Files"/>
</p>

#### Enabling IIS in Windows with CGI.
<p>
<img src="https://i.imgur.com/FfSgBEm.png" height="50%" width="50%" alt="IIS enabled with CGI"/>
</p>

#### Installation of PHP Manager for IIS.
<p>
<img src="https://i.imgur.com/NjUCRTc.png" height="50%" width="50%" alt="PHP Manager Installation"/>
</p>

#### Installation of Rewrite Module.
<p>
<img src="https://i.imgur.com/CSF9zS9.png" height="50%" width="50%" alt="Rewrite Module Installation"/>
</p>

#### Unzipping documents into newly created C:\PHP directory.
<p>
<img src="https://i.imgur.com/GdeJOxX.png" height="60%" width="60%" alt="PHP into newly created C:\PHP directory"/>
</p>

<br />

#### Part 3 (Continue With Download and Installation of Files, Install osTicket v1.15.8)
- Install VC_redist.x86.exe
- Install MySQL 5.5.62
    - Typical Setup -->
    - Launch Configuration Wizard -->
    - Standard Configuration -->
    - Password1
- Open IIS as an Admin and register PHP from within IIS
- Reload IIS (Open IIS, Stop and Start the Server)
- Install osTicket v1.15.8
    - Download osTicket from installation folder
    - Extract and copy "upload" folder to c:\inetpub\wwwroot
    - Within c:\inetpub\wwwroot, rename "upload" to "osTicket"
- Reload IIS (Open IIS, Stop and Start and the Server)
- Go to sites (inside IIS) --> Default --> osTicket
    - On the right, click "Browse *:80"
- Check extensions
    - Go back to IIS, Sites --> Default --> osTicket
    - Double-click PHP Manager
    - Click "Enable or disable an extension"
        - Enable: php_imap.dll
        - Enable: php_intl.dll
        - Enable: php_opcache.dll
    - Refresh the osTicket site in your browser.

<br />

#### Installation of VC_redist.x86.exe .
<p>
<img src="https://i.imgur.com/TVHwvy3.png" height="50%" width="50%" alt="VC_redist installed"/>
</p>

#### Installation of MySQL.
<p>
<img src="https://i.imgur.com/k134jlk.png" height="50%" width="50%" alt="MySQL installed"/>
</p>

#### Registration of PHP within IIS.
<p>
<img src="https://i.imgur.com/zsBPD6x.png" height="50%" width="50%" alt="PHP registration in IIS"/>
</p>

#### osTicket Installed in c:\inetpub\wwwroot.
<p>
<img src="https://i.imgur.com/OZtZocg.png" height="50%" width="50%" alt="osTicket installed"/>
</p>

#### "Browse *:80" in IIS.
<p>
<img src="https://i.imgur.com/IX5APUN.png" height="50%" width="50%" alt="Browse *:80 in IIS"/>
</p>

#### Enabling Extensions inside IIS.
<p>
<img src="https://i.imgur.com/oXOQcwk.png" height="50%" width="50%" alt="Extensions Enabled"/>
</p>

#### osTicket Istaller in browser.
<p>
<img src="https://i.imgur.com/ppCWGko.png" height="50%" width="50%" alt="osTicket Installer in browser"/>
</p>

</br>

#### Part 4 (osTicket and Heidi SQL installation)
- Rename to: ost-config.php
    - From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
    - To: C:\inetpub\wwwroot\osTicket\include\ost-config.php
- Assign Permissions: ost-config.php
    - Disable inheritance --> Remove All
    - New Permissions --> Everyone --> All
- Continue Setting Up osTicket in the browser (click "Continue")
    - Name the Helpdesk
    - Default email (receives email from the customers)
- Install HeidiSQL
    - Open Heidi SQL
    - Create a new session, (username: root | password: Password1)
    - Connect to the session
    - Create a database called "osTicket"
- Continue setting up osTicket in the browser
    - MySQL Database: osTicket
    - MySQL username: root
    - MySQL password: Password1
    - Click "Install Now!"
- osTicket access
    - Browse to help desk login page: http://localhost/osTicket/scp/login.php
    - End Users osTicket: http://localhost/osTicket/
- Clean up!
    - Delete: C:\inetpub\wwwroot\osTicket\setup
    - Set Permissions to "Read Only" for: C:\inetpub\wwwroot\osTicket\include\ost-config.php

<br />

#### ost-sampleconfig.php renamed to ost-config.php.
<p>
<img src="https://i.imgur.com/gvM9ChM.png" height="50%" width="50%" alt="Renamed to ost-config.php"/>
</p>

#### Permissions Assigned to ost-config.php.
<p>
<img src="https://i.imgur.com/y0Y6bOX.png" height="50%" width="50%" alt="Permissions assigned"/>
</p>

#### osTicket Basic Information and Installation.
<p>
<img src="https://i.imgur.com/SBo8GAJ.png" height="50%" width="50%" alt="Basic information for osTicket Installation"/>
</p>

#### Heidi SQL Installed and osTicket Database created.
<p>
<img src="https://i.imgur.com/5nppsO7.png" height="50%" width="50%" alt="osTicket Database created in Heidi SQL"/>
</p>

#### osTicket Successfully Installed.
<p>
<img src="https://i.imgur.com/CvRQlKj.png" height="50%" width="50%" alt="osTicket Installed"/>
</p>

#### Admin login for osTicket.
<p>
<img src="https://i.imgur.com/JcQHRRp.png" height="50%" width="50%" alt="Admin Page"/>
</p>

#### End User login for osTicket.
<p>
<img src="https://i.imgur.com/i8ThwtD.png" height="50%" width="50%" alt="End User Page"/>
</p>

