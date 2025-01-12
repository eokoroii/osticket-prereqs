<p align="center">
  <!-- Replace this image with something relevant to osTicket or your own custom banner -->
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo" width="300"/>
</p>

<h1>osTicket - Prerequisites & Installation Lab</h1>

<h2>Project Summary</h2>
<p>
  This lab demonstrates how I deployed a Windows 10 virtual machine in Microsoft Azure, 
  installed and configured IIS, PHP, MySQL, and then set up the open-source help desk system 
  <strong>osTicket</strong>. Throughout this process, I gained hands-on experience with Azure VMs, 
  web server configuration, and database setup. I also tested the final installation by creating 
  and managing support tickets within the osTicket environment.
</p>

<ul>
  <li>
    <strong>Operating Systems & Languages:</strong>
    <ul>
      <li>Windows 10 (21H2) on Azure</li>
      <li>PowerShell commands (for VM & network checks)</li>
      <li>PHP & MySQL for the osTicket backend</li>
    </ul>
  </li>
  <li>
    <strong>Environments & Services:</strong>
    <ul>
      <li>Azure Portal (Resource Groups, Virtual Machines)</li>
      <li>Remote Desktop Protocol (RDP)</li>
      <li>Internet Information Services (IIS)</li>
      <li>MySQL Community Server</li>
    </ul>
  </li>
  <li>
    <strong>Technologies:</strong>
    <ul>
      <li>osTicket (help desk ticketing system)</li>
      <li>PHP Manager for IIS</li>
      <li>Web Configuration & Permissions</li>
    </ul>
  </li>
</ul>

<hr />

<h2>Steps & Screenshots</h2>
<ol>
  <li>
    <strong>Create a Windows 10 VM in Microsoft Azure</strong><br />
    I created a new Resource Group named <code>osTicket</code> using East US 2,
    then deployed a Windows 10 virtual machine. Once configured, I connected via RDP to manage 
    the operating system and proceed with the lab.
    <br /><br />
    <p align="center">
    <img src="https://i.imgur.com/0YDE2fS.png" alt="Azure VM Creation" width="600" />
    </p>
  </li>
  <br />

  <li>
    <strong>Enable IIS (Internet Information Services)</strong><br />
    On the Windows 10 VM, I navigated to <em>Control Panel &gt; Programs &gt; Turn Windows features on or off</em>, 
    then enabled IIS along with all required web server features. This step ensures the VM can host a local website 
    to run osTicket.
    <br /><br />
    <p align="center">
    <img src="https://i.imgur.com/1bAfSdH.png" alt="Enable IIS Features" width="600" />
    </p>
  </li>
  <br />

  <li>
    <strong>Install PHP Manager & MySQL</strong><br />
    I installed <strong>PHP Manager for IIS</strong> and <strong>MySQL Community Server</strong>. 
    Configuring MySQL with a root password allowed osTicket to connect to the database for storing ticket and user information.
    <br /><br />
    <p align="center">
    <img src="https://i.imgur.com/qu2uram.png" alt="PHP Manager Installation" width="600" />
    <br /><br />
    <img src="https://i.imgur.com/vugsBem.png" alt="MySQL Installation" width="600" />
    </p>
  </li>
  <br />

  <li>
    <strong>Download and Configure osTicket</strong><br />
    After downloading osTicket from the official website, I extracted the files into 
    <code>C:\inetpub\wwwroot\osticket</code>. I renamed <code>ost-sampleconfig.php</code> to <code>ost-config.php</code> 
    and entered my MySQL credentials. Finally, I gave <code>IIS_IUSRS</code> write permissions on the config file to allow 
    the installer to complete.
    <br /><br />
    <p align="center">
    <img src="https://i.imgur.com/4UwcJeS.png" alt="Extract osTicket Files" width="600" />
    <br /><br />
    <img src="https://i.imgur.com/VpZd2Ty.png" alt="ost-config.php Setup" width="600" />
    </p>
  </li>
  <br />

  <li>
    <strong>Run the osTicket Installation Wizard</strong><br />
    Using a web browser, I navigated to <code>http://&lt;PublicIP&gt;/osticket/</code>. The installation wizard 
    let me configure the database connection, create the admin account, and finalize my help desk settings. 
    Once the setup completed, I removed write permissions from <code>ost-config.php</code> for security.
    <br /><br />
    <p align="center">
    <img src="https://i.imgur.com/MAGmeJT.png" alt="osTicket Setup Wizard" width="600" />
    <br /><br />
    <img src="https://i.imgur.com/9TUO8h5.png" alt="osTicket Installation Complete" width="600" />
    </p>
  </li>
  <br />

  <li>
    <strong>Testing the Help Desk</strong><br />
    Lastly, I confirmed everything worked by logging into the osTicket Admin Panel, creating a test user ticket, 
    and ensuring the system handled ticket creation and assignment successfully.
    <br /><br />
    <p align="center">
    <img src="https://i.imgur.com/PgqWruI.png" alt="Admin Panel Dashboard" width="600" />
    <br /><br />
    <img src="https://i.imgur.com/eMhNhSE.png" alt="Ticket Creation" width="600" />
    </p>
  </li>
</ol>

<hr />

<h2>Conclusion</h2>
<p>
  Through this lab, I learned how to configure a cloud-hosted Windows environment in Azure, install and configure 
  the necessary web stack components (IIS, PHP, MySQL), and deploy the osTicket help desk platform. 
  This hands-on experience showcased the importance of correct file permissions, database integration, and 
  user account management for a successful ticketing system.
</p>
