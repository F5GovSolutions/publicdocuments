Lab Instructions for SWG Explict Forward Proxy
==============================================

Task 1. Test browing websites
-----------------------------

  #. Open Chrome or Firefox.

  #. Select Wikipedia bookmark in the Favorites Bar.

  #. Now open new tabs and select a differen bookmark for each site, [e.g. ESPN, Draftkings, Chatgpt, etc.) bookmark.

  What is the result of browsing to each of these sites?

  #. Open Windows Settings.

  #. Search for and select Proxy and review the proxy settings by clicking the Edit button.

    The F5 Explicit Forward proxy has already been configured for the browsers to use in the operating system.

  #. Turn off the 'Use a proxy server' setting. 

  #. Go back to your browser and click on the ESPN and or Draftkings bookmark again.


Task 2. - Test SFTP client - FileZilla
--------------------------------------

  #. Open FileZilla

  `filezilla <./images/t2-fz-1.png>`__

  #. Before connecting anywhere, select 'Desktop' under 'Local site'. The local folder now is the Desktop of this remote PC.

  #. Click the 'Site Manager' icon or Select it under File menu.

  #. Click the 'Connect' button
  
    Watch connection and negotiation in the status pane. It should connect to the site and you should see the list of files on the right site; 'Remote site' pane.

  `filezilla connect <./images/t2-fz-2.png>`__

  #. Copy over the 'Readme.txt file to the PC.  You can either Double click it or drag the file in Remote site folder to the Local site folder or to the Windows Desktop.

Open the file view it's contents.

![file open](./images/t2-fz-3.png)

**Step 6.** View the SOCKS Proxy settings in the FileZilla client, by selecting the Settings menu under Edit. Then choose General Proxy in the left navigation pain.

![fileZilla proxy](./images/t2-fz-2.png)


## Task 3 - Test SSH client through explicit proxy

**Step 1.** Open the PuTTY ssh client.

**Step 2.** Type the site **test.rebex.net** into the **Host Name** field and press Open

![putty client](./images/t3-ssh-1a.png)

The connection will fail with a message: "Network error: Permission denied"

**Step 3.** Select test.rebex.net in the Saved Sessions section and press Open

**Step 4.** 


