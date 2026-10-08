<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

# osTicket Installation Guide

## Overview

This guide explains how to install and configure **osTicket** on a Windows machine using:

* Windows
* IIS (Internet Information Services)
* PHP
* MySQL
* PHP Manager for IIS
* IIS URL Rewrite Module
* HeidiSQL
* osTicket

By the end of this guide, you will have a working osTicket help desk to create and manage IT support tickets.

---

# 1. Installation Files

Before beginning, make sure the following installation files are available on your machine.

You should have:

* `osTicket-v1.15.8.zip`
* `php-7.3.8-nts-Win32-VC15-x86.zip`
* `PHPManagerForIIS_V1.5.0.msi`
* `rewrite_amd64_en-US.msi`
* `VC_redist.x86.exe`
* `mysql-5.5.62-win32.msi`
* `HeidiSQL` installer

All the files needed are available [here](https://tinyurl.com/4p3h29sm)
> **Note:** The versions above are the versions used for this installation project.

---

# 2. Extract the Installation Files

1. Download the provided installation files to the Windows VM.
2. Locate the downloaded ZIP files.
3. Right-click the ZIP file and select **Extract All**.
4. Extract the files to an easy-to-access location.

For example:

```text
C:\Desktop\osTicket-Installation-Files
```
<img width="1124" height="634" alt="1" src="https://github.com/user-attachments/assets/48ea219e-d6a3-4bfe-93b0-5dd6213c67fe" />

---

# 3. Enable IIS and CGI

IIS (Internet Information Services) will be used to host the osTicket website.

### Open Windows Features

1. Open **Control Panel**.
2. Select **Programs and Features**.
3. Click **Turn Windows features on or off**.
4. Find:

```text
Internet Information Services
```
<img width="1131" height="633" alt="2" src="https://github.com/user-attachments/assets/a9c04ff6-c123-48f1-a6fd-575b0c00491e" />

5. Expand:

```text
Internet Information Services
└── World Wide Web Services
    └── Application Development Features
```

6. Enable:

```text
CGI
```

7. Click **OK**.

<img width="1309" height="824" alt="3" src="https://github.com/user-attachments/assets/6d681d99-3c82-4042-9369-027d7cfd1bae" />

Windows will install the required IIS components. This may take several minutes.

---

# 4. Install PHP Manager for IIS

Navigate to your installation files and run:

```text
PHPManagerForIIS_V1.5.0.msi
```
<img width="1122" height="633" alt="4" src="https://github.com/user-attachments/assets/af4ec364-c22a-42ac-812e-2bc5451d12d6" />


Follow the installation wizard and accept the default options.

PHP Manager lets IIS manage and configure PHP.

---

# 5. Install the IIS URL Rewrite Module

Run:

```text
rewrite_amd64_en-US.msi
```
<img width="1125" height="632" alt="5" src="https://github.com/user-attachments/assets/427ceadb-ba98-4bfe-ada8-3a364e60faec" />


Follow the installation wizard and accept the default settings.

The URL Rewrite module allows IIS to process URL rewriting rules used by web applications.

---

# 6. Install PHP

### Create the PHP folder

Open:

```text
C:\
```

Create a new folder named:

```text
PHP
```

Your folder should look like:

```text
C:\PHP
```

<img width="1122" height="632" alt="6" src="https://github.com/user-attachments/assets/a8935ad4-621a-4e56-9512-13c41229f6dd" />


### Extract PHP

Locate in the installation files:

```text
php-7.3.8-nts-Win32-VC15-x86.zip
```

Extract its contents into:

```text
C:\PHP
```

After extraction, the PHP executable should be located at:

```text
C:\PHP\php-cgi.exe
```

---

# 7. Install Visual C++ Redistributable

From the installation files, run:

```text
VC_redist.x86.exe
```

Follow the installation wizard.

This installs the Microsoft Visual C++ runtime required by PHP.

---

# 8. Install MySQL

Run:

```text
mysql-5.5.62-win32.msi
```

### Installation settings

When asked for the setup type, select:

```text
Typical
```
<img width="493" height="384" alt="7" src="https://github.com/user-attachments/assets/6ff8e24b-2838-4a7c-9aac-c2fc5f70898e" />

Continue through the installation.

When installation finishes, make sure:

```text
Launch the MySQL Instance Configuration Wizard
```

is checked.

<img width="492" height="388" alt="8" src="https://github.com/user-attachments/assets/639f5169-ed81-4026-ae2d-5feaff220df7" />

Click **Finish**.

---

# 9. Configure MySQL

The MySQL Server Instance Configuration Wizard will open.

### Configuration Type

Select:

```text
Standard Configuration
```
<img width="499" height="379" alt="9" src="https://github.com/user-attachments/assets/829ed70b-8d68-4406-a13d-a94f3b934dee" />

Continue through the wizard.

### Create the Root Password

When prompted for a MySQL root password, create a password that you will remember.

<img width="500" height="384" alt="10" src="https://github.com/user-attachments/assets/49a948cc-4100-4427-8261-dcc891fc0a0d" />

> **Important:** Keep this password secure. You will need it later when configuring the osTicket database.

Click:

```text
Execute
```

Wait for the configuration process to finish.

Then click:

```text
Finish
```

---

# 10. Open IIS Manager

Open the Windows Start menu and search for:

```text
IIS
```

Open:

```text
Internet Information Services (IIS) Manager
```

Run IIS Manager as **Administrator**.

<img width="834" height="468" alt="11" src="https://github.com/user-attachments/assets/aa866fc3-4e38-4b4d-bee3-9bb1a77526fb" />

---


# 11. Register PHP with IIS

Inside IIS Manager:

1. Select the server in the left panel.
2. Open:

```text
PHP Manager
```

3. Select:

```text
Register new PHP version
```

4. Click the `...` button.
5. Navigate to:

```text
C:\PHP
```

6. Select:

```text
php-cgi.exe
```

7. Click **OK**.

PHP is now registered with IIS.

---

# 12. Restart IIS

Restart the IIS server.

In IIS Manager:

1. Select the server.
2. Click **Restart** under **Manage Server**.

You can also right-click the server and select:

```text
Stop
```

followed by:

```text
Start
```

---

# 13. Install osTicket

Locate from the Installation files:

```text
osTicket-v1.15.8.zip
```

Extract the ZIP file.

Inside the extracted folder you will find:

```text
upload
```

Copy the `upload` folder to:

```text
C:\inetpub\wwwroot
```

Rename the folder:

```text
upload
```

to:

```text
osTicket
```

Your osTicket installation should now be located at:

```text
C:\inetpub\wwwroot\osTicket
```

<img width="1122" height="631" alt="12" src="https://github.com/user-attachments/assets/7a4252b3-d482-4cb1-9e33-32b70425f250" />

---

# 14. Configure PHP Extensions

Restart IIS again.

In IIS Manager, navigate to:

```text
Sites
└── Default Web Site
    └── osTicket
```

Select the `osTicket` site.

Click:

```text
Browse *.80 (http)
```

<img width="1208" height="700" alt="13" src="https://github.com/user-attachments/assets/984c98a0-5677-4179-abc6-5adab1a5f24c" />

This should open osTicket in your web browser.

At this point, the osTicket installer may report that some PHP extensions are missing.

### Enable the Required Extensions

Return to IIS Manager.

Navigate to:

```text
Sites
└── Default Web Site
    └── osTicket
```

Double-click:

```text
PHP Manager
```

Select:

```text
Enable or disable an extension
```

<img width="1210" height="698" alt="14" src="https://github.com/user-attachments/assets/56eb12a9-4a2d-4048-8053-6beb722b5b99" />

Enable the following extensions:

```text
php_imap.dll
php_intl.dll
php_opcache.dll
```

<img width="1211" height="694" alt="15" src="https://github.com/user-attachments/assets/57dca1f5-3a9d-4ca4-b1eb-b4055afb62cf" />

After enabling the extensions, refresh the osTicket installation page in your browser.

The required extensions should now be enabled.

---

# 15. Configure the osTicket Configuration File

osTicket provides a sample configuration file that must be renamed before installation.

Navigate to:

```text
C:\inetpub\wwwroot\osTicket\include
```

Find:

```text
ost-sampleconfig.php
```

Rename it to:

```text
ost-config.php
```

The final path should be:

```text
C:\inetpub\wwwroot\osTicket\include\ost-config.php
```

<img width="1123" height="631" alt="16" src="https://github.com/user-attachments/assets/a46f5c74-426e-42eb-bd60-579616fe1009" />

---

## Configure File Permissions

The osTicket installer needs permission to modify the configuration file.

Right-click:

```text
ost-config.php
```

Select:

```text
Properties → Security → Advanced
```

Disable inheritance and remove the inherited permissions.

Add a new permission for:

```text
Everyone
```

<img width="766" height="519" alt="17" src="https://github.com/user-attachments/assets/8c69b0d2-9539-4df1-859f-1c7943a2bf06" />

Give it the required permissions for the installation.

> **Security Note:** Granting broad permissions such as **Full Control** to `Everyone` is useful for a lab environment, but it is **not recommended for a production server**. Production systems should use the minimum permissions necessary.

---

# 16. Create the osTicket Database

osTicket requires a MySQL database to store tickets, users, settings, and other application data.

Install:

```text
HeidiSQL
```

from the installation files.

During installation, select:

```text
Launch HeidiSQL
```
<img width="601" height="464" alt="18" src="https://github.com/user-attachments/assets/f232de7d-b29c-49f1-a080-fdd31ded6204" />

when prompted.

---

## Connect to MySQL

When HeidiSQL opens:

1. Create a new session.
2. Enter the MySQL credentials created during the MySQL installation.
3. Enter the appropriate username and password.
4. Click **Open**.

<img width="684" height="482" alt="19" src="https://github.com/user-attachments/assets/c3a887d9-9a20-469f-a2e1-bfea35082853" />

---

## Create the Database

After connecting:

1. Right-click the MySQL server/session.
2. Select:

```text
Create new → Database
```

3. Name the database:

```text
osTicket
```

4. Click **OK**.

Your osTicket database has now been created.

---

# 17. Complete the osTicket Installation

Return to the osTicket installation page in your browser.

The installer will ask for information about:

* Helpdesk name
* Default email
* Administrator account
* MySQL database
* Database username
* Database password
* Database name

For the database section, enter the information you configured in MySQL and HeidiSQL.

For example:

```text
Database Name: osTicket
Database User: root
Database Password: <your MySQL password>
```

<img width="823" height="1221" alt="20" src="https://github.com/user-attachments/assets/14814470-9cef-47e5-8693-d86d2f897ed7" />


Review the installation settings.

When everything looks correct, click:

```text
Install Now
```

---

# 18. Installation Complete

If the installation was successful, osTicket should now be installed and running on your IIS server.

<img width="823" height="638" alt="21" src="https://github.com/user-attachments/assets/0ba95e1d-9a0d-4eb2-a2b8-c69157320e07" />

You can use the following URLs to access your installation.

### osTicket Helpdesk

```text
http://localhost/osTicket/
```

This is where users can create support tickets.

### osTicket Staff/Admin Panel

```text
http://localhost/osTicket/scp/login.php
```

This is where IT staff can log in and manage tickets.

---

# 19. Installation Summary

The installation process can be summarized as:

```text
Windows VM
    ↓
Install IIS + CGI
    ↓
Install PHP Manager
    ↓
Install URL Rewrite
    ↓
Install PHP
    ↓
Install Visual C++ Redistributable
    ↓
Install MySQL
    ↓
Configure MySQL
    ↓
Register PHP with IIS
    ↓
Install osTicket
    ↓
Enable PHP Extensions
    ↓
Configure ost-config.php
    ↓
Create MySQL Database
    ↓
Run osTicket Installer
    ↓
Test Helpdesk
```

---

# 20. Troubleshooting

### osTicket says PHP is missing

Verify that PHP is installed in:

```text
C:\PHP
```

and that IIS is registered to use:

```text
C:\PHP\php-cgi.exe
```

### PHP extensions are missing

Open:

```text
IIS Manager → osTicket → PHP Manager
```

Select:

```text
Enable or disable an extension
```

Verify that the required extensions are enabled.

### The osTicket website does not load

Verify that:

* IIS is running.
* The osTicket folder exists at:

```text
C:\inetpub\wwwroot\osTicket
```

* The Default Web Site is running.
* PHP is registered correctly.
* IIS has been restarted after configuration changes.

### Database connection fails

Verify that:

* MySQL is running.
* The database is named:

```text
osTicket
```

* The database username is correct.
* The database password is correct.
* HeidiSQL can successfully connect to the MySQL server.

---

# Conclusion

Congratulations! You have successfully installed osTicket on a Windows VM using IIS, PHP, and MySQL.

This environment can now be used as a basic **IT help desk/ticketing system** for practicing:

* Ticket management
* User support
* Troubleshooting
* Incident documentation
* Help desk workflows
* IT service management

