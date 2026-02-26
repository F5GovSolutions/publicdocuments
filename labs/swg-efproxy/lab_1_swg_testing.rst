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

    .. image:: ./images/t2-fz-1.png
        :align: center
        :alt: filezilla

  #. Before connecting anywhere, select 'Desktop' under 'Local site'. The local folder now is the Desktop of this remote PC.

  #. Click the 'Site Manager' icon or Select it under File menu.

  #. Click the 'Connect' button
  
    Watch connection and negotiation in the status pane. It should connect to the site and you should see the list of files on the right site; 'Remote site' pane.

    .. image:: ./images/t2-fz-2.png
        :align: center
        :alt: filezilla connect

  #. Copy over the 'Readme.txt file to the PC.  You can either Double click it or drag the file in Remote site folder to the Local site folder or to the Windows Desktop.

Open the file view it's contents.

    .. image:: ./images/t2-fz-3.png
        :align: center
        :alt: file open

  #. View the SOCKS Proxy settings in the FileZilla client, by selecting the Settings menu under Edit. Then choose General Proxy in the left navigation pain.

    .. image:: ./images/t2-fz-4.png
        :align: center
        :alt: filezilla proxy

Task 3 - Test SSH client through explicit proxy
-----------------------------------------------

  #. Open the PuTTY ssh client.

  #. Type the site **test.rebex.net** into the **Host Name** field and press Open

    .. image:: ./images/t3-ssh-1a.png
        :align: center
        :alt: putty client

    The connection will fail with a message: "Network error: Permission denied"

  #. Select test.rebex.net in the Saved Sessions section and press Load. Then select the Connection > Proxy category in the left navigation pane.

    .. image:: ./images/t3-ssh-2.png
        :align: center
        :alt: putty proxy settings

  #. View the proxy settings. The PuTTY client is configured to use the F5 Explicit Forward Proxy for SSH connections, which is why the connection failed in the previous step.
  

