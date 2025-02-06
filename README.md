<h1>osTicket Lab 1: Installation on Windows IIS</h1>

<h2>Project Summary</h2>
<p>
  In this section of my osTicket labs, I demonstrate how I deployed osTicket 
  on a Windows Server VM in Azure. It covers installing IIS, PHP, MySQL, 
  and finalizing the osTicket web installer.
</p>

<ul>
  <li><strong>Key Components:</strong>
    <ul>
      <li>Azure Windows Server VM</li>
      <li>IIS (Internet Information Services)</li>
      <li>PHP &amp; MySQL</li>
      <li>HeidiSQL for DB management</li>
      <li>osTicket v1.15.8</li>
    </ul>
  </li>
  <li><strong>Goal:</strong> 
    Set up a functional ticketing platform ready for admin configuration and end-user ticket creation.
  </li>
</ul>

<hr />

<h2>Steps & Screenshots</h2>
<ol>
  <li>
    <strong>Create &amp; RDP into Windows Server VM</strong><br />
    I spun up a Windows Server (2019 or 2022) VM in Azure, ensuring RDP port 3389 was open. 
    After deployment, I noted the Public IP and connected via Remote Desktop.
    <br /><br />
    <p align="center">
      <img src="https://i.imgur.com/gzzmKTf.png" alt="Windows Server VM creation" width="600" />
      <br />
      <em>Figure 2.1 – Windows Server VM in Azure.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>Enable IIS &amp; Required Features</strong><br />
    In <em>Control Panel &gt; Programs &gt; Turn Windows features on or off</em>, 
    I enabled:
    <ul>
      <li>IIS (Web Server)</li>
      <li>World Wide Web Services</li>
      <li>Application Development Features (CGI)</li>
    </ul>
    <p align="center">
      <img src="https://i.imgur.com/dbBWfPq.png" alt="Enabling IIS features" width="600" />
      <br />
      <em>Figure 2.2 – Enabling IIS and other Windows features.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>Installing PHP Manager, Rewrite Module</strong><br />
    From my <em>osTicket-Installation-Files</em> package, I installed:
    <ul>
      <li>PHP Manager for IIS</li>
      <li>IIS Rewrite Module</li>
      <li>VC_redist.x86 (if needed)</li>
    </ul>
    <p align="center">
      <img src="https://i.imgur.com/cUaPXi2.png" alt="PHP Manager install" width="600" />
      <img src="https://i.imgur.com/FG0jmbE.png" alt="Rewrite Module install" width="600" />
      <br />
      <em>Figure 2.3 – Installing PHP Manager &amp; Rewrite Module.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>Extract &amp; Configure PHP</strong><br />
    I created <code>C:\PHP</code> and unzipped <em>php-7.3.8-nts-Win32-VC15-x86.zip</em> into it. 
    Then, from <em>IIS Manager &gt; PHP Manager</em>, I registered <code>php-cgi.exe</code>.
    <br /><br />
    <p align="center">
      <img src="https://i.imgur.com/pKYbeZh.png" alt="Creating C:\PHP" width="600" />
      <img src="https://i.imgur.com/6XS84xs.png" alt="extracting php-7.3.8-nts-Wi32-VC15-x86.zip" width="600" />
      <img src="https://i.imgur.com/Mh4O7Z7.png" alt="PHP in IIS" width="600" />
      <br />
      <em>Figure 2.4 – Registering PHP in IIS Manager.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>Install MySQL (Typical Setup)</strong><br />
    I downloaded MySQL, ran the installer, and set the root password. 
    This gives osTicket a database for storing tickets and configurations.
    <br /><br />
    <p align="center">
      <img src="https://i.imgur.com/SG7QplV.png" alt="MySQL installation wizard" width="600" />
      <br />
      <em>Figure 2.5 – Configuring MySQL root credentials.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>Install HeidiSQL</strong><br />
    HeidiSQL makes database management simple. I installed it to create and manage the <code>osTicket</code> database. 
    <br /><br />
    <p align="center">
      <img src="https://i.imgur.com/WmAqfnS.png" alt="HeidiSQL installation" width="600" />
      <br />
      <em>Figure 2.6 – Installing HeidiSQL.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>Unzip &amp; Deploy osTicket Files</strong><br />
    From the <em>osTicket-v1.15.8.zip</em> package, I unzipped the contents into <code>C:\inetpub\wwwroot</code> 
    and renamed the <em>upload</em> folder to <em>osTicket</em>.
    <br /><br />
    <p align="center">
      <img src="https://i.imgur.com/njN8059.png" alt="osTicket files in IIS" width="600" />
      <br />
      <em>Figure 2.7 – Placing osTicket files in wwwroot.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>First Look at osTicket Installer</strong><br />
    In IIS Manager, under <em>Default Web Site &gt; osTicket</em>, I selected <em>Browse *:80</em>. 
    This opened the osTicket installer page in my browser.
    <br /><br />
    <p align="center">
      <img src="https://i.imgur.com/Ax5IPcM.png" alt="osTicket initial installer" width="600" />
      <br />
      <em>Figure 2.8 – osTicket installation welcome page.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>Enable PHP Extensions</strong><br />
    Within <em>PHP Manager &gt; Enable or disable an extension</em>, 
    I enabled <code>php_imap.dll</code>, <code>php_intl.dll</code>, and <code>php_opcache.dll</code> 
    to remove warnings in the installer.
    <br /><br />
    <p align="center">
      <img src="https://i.imgur.com/kgLN0ZY.png" alt="PHP extension settings" width="600" />
      <br />
      <em>Figure 2.9 – Confirming required PHP extensions are active.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>Configure ost-config.php</strong><br />
    I renamed <code>ost-sampleconfig.php</code> to <code>ost-config.php</code> and 
    adjusted its file permissions so the installer could write to it.
    <br /><br />
    <p align="center">
      <img src="https://i.imgur.com/zque2y6.png" alt="Editing file security" width="600" />
      <br />
      <em>Figure 2.10 – Setting file permissions for ost-config.php.</em>
    </p>
  </li>
  <br />

  <li>
    <strong>Create Database &amp; Complete Installation</strong><br />
    Using HeidiSQL, I created a database named <code>osTicket</code>. Then, in the web installer, 
    I specified the DB name, root credentials, and completed the installation. 
    <br /><br />
    <p align="center">
      <img src="https://i.imgur.com/Y1U78QQ.png" alt="Creating osTicket DB" width="600" />
      <br />
      <em>Figure 2.11 – Database creation in HeidiSQL.</em>
      <br /><br />
      <img src="https://i.imgur.com/DFplE5y.png" alt="osTicket final install success" width="600" />
      <br />
      <em>Figure 2.12 – osTicket successfully installed!</em>
    </p>
  </li>
</ol>

<hr />

<h2>Conclusion</h2>
<p>
  At this point, osTicket is fully operational on my Windows Server VM. I can log in as an admin, 
  configure departments, create tickets, and more. This sets the stage for deeper 
  help desk management labs, covered in the next sections.
</p>
