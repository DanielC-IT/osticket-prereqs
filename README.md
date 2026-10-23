
<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo" />
</p>

# osTicket Installation and Configuration on Windows 11

## Project Overview

This project demonstrates the installation and configuration of **osTicket**, an open-source help desk ticketing system, on a Windows 11 machine using IIS, PHP, and MySQL. The demonstration covers preparing the Windows environment, configuring the web server and database, resolving PHP extension requirements, and completing the osTicket setup.

## Environment and Technologies Used

- **Operating system:** Windows 11
- **Web server:** Internet Information Services (IIS)
- **Scripting runtime:** PHP 7.3.8 Non-Thread Safe (NTS), 32-bit
- **Database server:** MySQL 5.5.62
- **PHP/IIS management:** PHP Manager for IIS
- **IIS component:** URL Rewrite Module
- **Database client:** HeidiSQL
- **Help desk application:** osTicket 1.15.8

## Installation Files

The following installation files were used:

- `osTicket-v1.15.8.zip`
- `php-7.3.8-nts-Win32-VC15-x86.zip`
- `PHPManagerForIIS_V1.5.0.msi`
- `rewrite_amd64_en-US.msi`
- `VC_redist.x86.exe`
- `mysql-5.5.62-win32.msi`
- HeidiSQL installer

The files used for this lab are collected here: [Installation files](https://tinyurl.com/4p3h29sm).

## Demonstration

### 1. Prepare the Installation Files

1. Download the installation files listed above.
2. Open the folder containing the downloaded files.
3. For each ZIP archive, right-click the file and select **Extract All**.
4. Extract the files to an easy-to-access working folder, such as `C:\Desktop\osTicket-Installation-Files`.

<img width="1124" alt="Installation files extracted to a working folder" src="https://github.com/user-attachments/assets/48ea219e-d6a3-4bfe-93b0-5dd6213c67fe" />

### 2. Enable IIS and CGI

IIS hosts the osTicket website. The CGI feature allows IIS to run PHP through FastCGI.

1. Open **Control Panel**.
2. Select **Programs and Features**, then choose **Turn Windows features on or off**.
3. Expand **Internet Information Services**.
4. Expand **World Wide Web Services → Application Development Features**.
5. Select **CGI**, then click **OK**.
6. Allow Windows to install the selected components.

<img width="1131" alt="Windows Features showing Internet Information Services" src="https://github.com/user-attachments/assets/a9c04ff6-c123-48f1-a6fd-575b0c00491e" />

<img width="1309" alt="CGI selected under IIS Application Development Features" src="https://github.com/user-attachments/assets/6d681d99-3c82-4042-9369-027d7cfd1bae" />

### 3. Install PHP Manager for IIS

PHP Manager adds PHP configuration options to IIS Manager.

1. Open the installation-files folder.
2. Double-click `PHPManagerForIIS_V1.5.0.msi`.
3. Follow the setup wizard and accept the options used for this lab.

<img width="1122" alt="PHP Manager for IIS installer" src="https://github.com/user-attachments/assets/af4ec364-c22a-42ac-812e-2bc5451d12d6" />

### 4. Install the IIS URL Rewrite Module

The URL Rewrite Module allows IIS to process URL rewriting rules used by web applications.

1. Open the installation-files folder.
2. Double-click `rewrite_amd64_en-US.msi`.
3. Follow the setup wizard to complete the installation.

<img width="1125" alt="IIS URL Rewrite Module installer" src="https://github.com/user-attachments/assets/427ceadb-ba98-4bfe-ada8-3a364e60faec" />

### 5. Install PHP

1. Open File Explorer and navigate to `C:\`.
2. Create a folder named `PHP`, so the full folder path is `C:\PHP`.
3. Locate `php-7.3.8-nts-Win32-VC15-x86.zip` in the installation-files folder.
4. Extract the archive contents into `C:\PHP`.
5. Confirm that `C:\PHP\php-cgi.exe` exists.

<img width="1122" alt="PHP folder created on the C drive" src="https://github.com/user-attachments/assets/a8935ad4-621a-4e56-9512-13c41229f6dd" />

<img width="1126" height="633" alt="image" src="https://github.com/user-attachments/assets/ac784da8-8e30-4413-afdb-0358c91c3d31" />


### 6. Install the Visual C++ Redistributable

PHP requires the matching Microsoft Visual C++ runtime.

1. Open the installation-files folder.
2. Double-click `VC_redist.x86.exe`.
3. Follow the installer prompts to complete the installation.

<img width="1122" height="631" alt="image" src="https://github.com/user-attachments/assets/7ae6905b-a4c6-4b57-8200-9ece87489ddb" />

<img width="481" height="298" alt="image" src="https://github.com/user-attachments/assets/67f7e278-33d9-4b50-b126-3f67c630f9ae" />



### 7. Install MySQL

1. Open the installation-files folder.
2. Double-click `mysql-5.5.62-win32.msi`.
3. Select **Typical** as the setup type and continue through the wizard.
4. When installation finishes, make sure **Launch the MySQL Instance Configuration Wizard** is selected.
5. Click **Finish** to open the configuration wizard.

<img width="493" alt="MySQL setup type selection" src="https://github.com/user-attachments/assets/6ff8e24b-2838-4a7c-9aac-c2fc5f70898e" />

<img width="492" alt="MySQL option to launch the instance configuration wizard" src="https://github.com/user-attachments/assets/639f5169-ed81-4026-ae2d-5feaff220df7" />

### 8. Configure MySQL

1. In the MySQL Server Instance Configuration Wizard, select **Standard Configuration**.
2. Continue through the wizard.
3. When prompted, set a MySQL root password and store it securely. You will need it when connecting to MySQL and configuring osTicket.
4. Click **Execute** and wait for the configuration tasks to finish.
5. Click **Finish**.

<img width="499" alt="MySQL standard configuration selection" src="https://github.com/user-attachments/assets/829ed70b-8d68-4406-a13d-a94f3b934dee" />

<img width="500" alt="MySQL root password configuration" src="https://github.com/user-attachments/assets/49a948cc-4100-4427-8261-dcc891fc0a0d" />

<img width="500" height="381" alt="image" src="https://github.com/user-attachments/assets/af7d382d-b8fa-45ed-ae6e-16146e3a5aa1" />

<img width="500" height="381" alt="image" src="https://github.com/user-attachments/assets/aeafed01-802f-4ae6-b2ab-e26220a3cedf" />


### 9. Open IIS Manager

1. Open the Windows **Start** menu.
2. Search for **IIS**.
3. Open **Internet Information Services (IIS) Manager**. Select **Run as administrator**.

<img width="834" alt="Internet Information Services (IIS) Manager open" src="https://github.com/user-attachments/assets/aa866fc3-4e38-4b4d-bee3-9bb1a77526fb" />

### 10. Register PHP with IIS

1. In IIS Manager, select the server in the left-hand **Connections** pane.
2. Open **PHP Manager**.
3. Select **Register new PHP version**.
4. Click the browse (`...`) button and navigate to `C:\PHP`.
5. Select `php-cgi.exe` and click **OK** to register PHP.

<img width="977" height="811" alt="image" src="https://github.com/user-attachments/assets/c7ec5b0b-1aad-49c5-a2ea-a8290e04c9ea" />

<img width="715" height="437" alt="image" src="https://github.com/user-attachments/assets/a6b16df6-9b9f-4cb8-9250-b7cab872478b" />

<img width="1186" height="713" alt="image" src="https://github.com/user-attachments/assets/5b56c4e6-a48c-4adf-9112-703f4dcb762b" />


### 11. Restart IIS

1. In IIS Manager, select the server in the **Connections** pane.
2. Under **Manage Server**, click **Restart**.
3. If **Restart** is unavailable, right-click the server and select **Stop**, then right-click it again and select **Start**.

<img width="966" height="343" alt="image" src="https://github.com/user-attachments/assets/8172fd02-45b5-4bd6-bdb6-eb6dc336e209" />


### 12. Place osTicket in the IIS Web Root

1. Locate `osTicket-v1.15.8.zip` in the installation-files folder.
2. Extract the ZIP archive.
3. Open the extracted folder and locate the `upload` directory.
4. Copy the `upload` directory to `C:\inetpub\wwwroot`.
5. Rename the copied folder from `upload` to `osTicket`.
6. Confirm that the application files are located at `C:\inetpub\wwwroot\osTicket`.

<img width="1122" alt="osTicket application folder in the IIS web root" src="https://github.com/user-attachments/assets/7a4252b3-d482-4cb1-9e33-32b70425f250" />

<img width="1125" height="634" alt="image" src="https://github.com/user-attachments/assets/96846480-c04b-4830-b01a-fccd4c4d3c05" />


### 13. Launch the osTicket Installer

This step configures the IIS site path and opens osTicket for the first time. The installer checks the PHP environment and identifies any required extensions that are not enabled.

1. Open **IIS Manager**.
2. In the **Connections** pane, expand **Sites → Default Web Site** and select **osTicket**.
3. In the **Actions** pane, select **Browse *.80 (http)** to open the application in a browser.
4. Review the osTicket setup page and note any missing PHP extensions displayed by the installer.

<img width="1208" alt="IIS Manager showing the osTicket application and Browse action" src="https://github.com/user-attachments/assets/984c98a0-5677-4179-abc6-5adab1a5f24c" />

<img width="824" height="766" alt="image" src="https://github.com/user-attachments/assets/c8bb3465-8edd-4382-8a7b-19f32aa42293" />


### 14. Enable the PHP Extensions Required by osTicket

Use the missing-extension list shown by the installer in Step 13 to identify what needs to be enabled.

1. Return to IIS Manager and select **Sites → Default Web Site → osTicket**.
2. Open **PHP Manager**.
3. Select **Enable or disable an extension**.
4. Enable the extensions required by this lab: `php_imap.dll`, `php_intl.dll`, and `php_opcache.dll`.
5. Return to the browser and refresh the osTicket installer page. Confirm that the missing-extension warnings have cleared.

<img width="1210" alt="PHP Manager extension configuration" src="https://github.com/user-attachments/assets/56eb12a9-4a2d-4048-8053-6beb722b5b99" />

<img width="1211" alt="PHP extensions enabled in PHP Manager" src="https://github.com/user-attachments/assets/57dca1f5-3a9d-4ca4-b1eb-b4055afb62cf" />

<img width="822" height="763" alt="image" src="https://github.com/user-attachments/assets/cb1a0e82-3b50-4808-b30b-6f5ff14491ec" />


### 15. Configure the osTicket Configuration File

osTicket uses a configuration file to store application settings. Rename the sample file before continuing with the installer.

1. In File Explorer, navigate to `C:\inetpub\wwwroot\osTicket\include`.
2. Find `ost-sampleconfig.php`.
3. Rename it to `ost-config.php`.
4. Confirm that the full path is `C:\inetpub\wwwroot\osTicket\include\ost-config.php`.

<img width="1123" alt="osTicket sample configuration file in the include folder" src="https://github.com/user-attachments/assets/a46f5c74-426e-42eb-bd60-579616fe1009" />

#### Set Configuration File Permissions

1. Right-click `ost-config.php` and select **Properties**.
2. Open the **Security** tab and select **Advanced**.
3. Configure the permissions required for the installer to write to the configuration file.
4. Use the minimum permissions needed for the lab and restore tighter permissions after installation if appropriate.

<img width="766" alt="Advanced security settings for ost-config.php" src="https://github.com/user-attachments/assets/8c69b0d2-9539-4df1-859f-1c7943a2bf06" />



### 16. Install HeidiSQL and Create the osTicket Database

osTicket needs a MySQL database to store tickets, users, configuration, and other application data.

1. Run the HeidiSQL installer from the installation-files folder.
2. Complete the setup and select **Launch HeidiSQL** if that option appears.

<img width="601" alt="HeidiSQL installer launch option" src="https://github.com/user-attachments/assets/f232de7d-b29c-49f1-a080-fdd31ded6204" />

#### Connect to MySQL

1. In HeidiSQL, create a new session.
2. Enter the connection details for the MySQL server configured in Step 8.
3. Enter the appropriate username and password.
4. Click **Open** to connect.

<img width="684" alt="HeidiSQL session connection settings" src="https://github.com/user-attachments/assets/c3a887d9-9a20-469f-a2e1-bfea35082853" />

#### Create the Database

1. In HeidiSQL, right-click the connected MySQL server or session.
2. Select **Create new → Database**.
3. Enter `osTicket` as the database name.
4. Click **OK**.
5. Confirm that `osTicket` appears in the database list.

<img width="936" height="593" alt="image" src="https://github.com/user-attachments/assets/f352d8c3-1e9e-4c8f-aea9-d77a02c12068" />

<img width="319" height="259" alt="image" src="https://github.com/user-attachments/assets/06c12d22-bd9f-4403-97bc-3fa8f9c46de5" />

<img width="936" height="593" alt="image" src="https://github.com/user-attachments/assets/5c7b0dc6-5cfc-4b8d-8edc-b326ad18afdf" />




### 17. Complete the osTicket Setup

1. Return to the osTicket installer in your browser.
2. Enter the help desk name and default email address.
3. Create the administrator account.
4. In the database section, enter the MySQL connection details and the database name created in Step 16.
5. Review the information and click **Install Now**.

For this lab, the database name is `osTicket`. Enter the database username and password that match your MySQL configuration.

<img width="823" alt="osTicket setup form" src="https://github.com/user-attachments/assets/14814470-9cef-47e5-8693-d86d2f897ed7" />

<!-- Add a screenshot here showing the installer submitting the configuration or reporting successful setup. Hide email addresses, passwords, and other sensitive values. -->

### 18. Verify the Installation

After the installer reports success, open the application and verify that both the help desk and staff login pages load.

- **Help desk:** `http://localhost/osTicket/`
- **Staff/admin login:** `http://localhost/osTicket/scp/login.php`

<img width="823" alt="osTicket installation success screen" src="https://github.com/user-attachments/assets/0ba95e1d-9a0d-4eb2-a2b8-c69157320e07" />

<!-- Add a screenshot here showing the help desk landing page and, if possible, a separate screenshot of the staff/admin login page. -->

