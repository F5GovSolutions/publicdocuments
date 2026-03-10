Lab 1. Testing the SWG Explict Forward Proxy
============================================

**Testing Web Traffic and Proxy Services with Client Applications**

In this Lab, you will use a Windows 11 client to test various web and network traffic scenarios configured through the BIG-IP system. These tests will show you how Secure Web Gateway (SWG) and Secure Sockets Layer Orchestrator (SSLO) work together to secure and manage different types of traffic.

The BIG-IP system is set up with the following key components:

- **SSLO with SWG Service**: This configuration integrates Secure Web Gateway with SSLO to inspect and filter outbound traffic. The SWG applies policies such as URL Filtering and Category-based rules to enforce secure and compliant access to web resources.

- **SSLO L3 Outbound Explicit Proxy Topology**: This Layer 3 outbound topology acts as an explicit proxy, routing traffic from the Windows 11 client through the BIG-IP system. It supports web traffic over HTTPS as well as other protocols via a SOCKS5 proxy.

Here are the activities you'll perform in this section:

1. **Browser Testing**: 
   - Use a web browser on the Windows 11 client to visit several websites.
   - You'll observe the SWG applies filtering rules, including allowing or blocking access based on URL Categories.

2. **SFTP Testing with FileZilla**:
   - Configure FileZilla to securely transfer files over SFTP.
   - The connection will be routed through the SOCKS5 proxy built on the SSLO L3 Outbound topology. This will help you validate the handling of secure file transfers over the proxy.

3. **SSH Testing with PuTTY**:
   - Use PuTTY to test SSH connections through the SOCKS5 proxy.
   - Review the proxy settings in PuTTY and verify the secure handling of SSH sessions.

These activities will give you hands-on experience with the SSLO Explicit Proxy topology and the SWG. You'll see how the system handles both web and non-web traffic securely and complies with policies.

Task 1. Browsing websites through the Explicit Forward Proxy
------------------------------------------------------------

    #. Log in to the Windows 11 client using the RDP or SuperJump Host access methods and open Chrome or Firefox.

    #. Select Wikipedia bookmark in the Favorites Bar.

    #. Now open new tabs and select a different bookmark for each tab, [e.g. ESPN, Draftkings, Chatgpt, etc.) bookmark.

        What is the result of browsing to each of these sites?

    #. Now open Windows Settings.

    #. Search for and open **Proxy settings**

        .. image:: ./images/l1-win-proxy-set.png
            :align: center
            :alt: win proxy settings
    
    #. Click the **Set up** button for the **Manual proxy setup** section to open the **Edit proxy server** page.

        .. image:: ./images/l1-win-proxy-on.png
            :align: center
            :alt: win proxy turn on

        Take note here the FQDN of the proxy server and the port.

    #. Turn **On** the 'Use a proxy server' setting and click **Save**.

    #. Go back to your browser and Refresh each of the tabs.  This can be done by clicking the browser Refresh button or using the CTRL + F5 shortcut to fully reload the webpage.

        What is the result of browsing to these sites now?

        .. image:: ./images/l1-win-proxy-block.png
            :align: center
            :alt: win proxy block

    #. Open a **Windows Command Prompt** and issue a ping to **proxy.f5labs.local**

        .. image:: ./images/l1-win-proxy-ip.png
            :align: center
            :alt: win proxy ip address

        Take note of the IP Address -- Also, recall the port used by the Proxy settings -- **3128**

    #. Now log into the **BIG-IP SSLO-1 TMUI** (refer back to `Lab Environment <./lab_environment.rst>`__ on how to log on) and navigate to **Local Traffic > Virtual Servers**

        .. image:: ./images/l1-ltm-vs.png
            :align: center
            :alt: vs proxy ip

        We can see that there is a Virtual Server that matches the IP and port used by the Windows 11 proxy settings. This means that the web traffic from the Windows 11 client is being sent to the BIG-IP system through the Explicit Proxy virtual server. The SSLO / SWG service will then apply its policies to this traffic, allowing or blocking access based on the URL categories and other rules configured in the system.

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

    #. View the SOCKS Proxy settings in the FileZilla client, by selecting the **Settings** menu under **Edit** main menu. Then choose **General Proxy** in the left navigation pane.

        .. image:: ./images/t2-fz-4.png
            :align: center
            :alt: filezilla proxy

Task 3 - Test SSH client through the Explicit Proxy
---------------------------------------------------

    #. Open the PuTTY ssh client.

    #. Type the site **test.rebex.net** into the **Host Name** field and press Open

        .. image:: ./images/t3-ssh-1.png
            :align: center
            :alt: putty client

        The connection will fail with a message: "Network error: Permission denied". This is expected because SSH is being blocked going out of the Windows 11 client.

    #. Reopen PuTTY again, and now select **test.rebex.net** in the **Saved Sessions** section and press **Load**. 
    
        PuTTY allows you to save connection profiles with the proxy settings already configured. 

    #. Then select the Connection > Proxy category in the left navigation pane.

        View the proxy settings. The PuTTY client is configured to use the F5 Explicit Forward Proxy for SSH connections using the SOCKS protocol on port 8080.

        .. image:: ./images/t3-ssh-load.png
            :align: center
            :alt: putty proxy settings

        .. image:: ./images/t3-ssh-proxy.png
            :align: center
            :alt: putty proxy settings view

    #. Press **Open** to initiate the connection to the SSH server again.

        When the connection is successful, you will be prompted to log in. Use the following credentials:
        - Username: demo

        - Password: password

        After logging in, you should see a command prompt. Type 'dir' or 'ls' command to list the files in the current directory; the same file is present in the directory we copied earlier.

    #. Type 'exit' to close the SSH connection when you are finished.

    #. Return to the BIG-IP TMUI and navigate to **Local Traffic > Virtual Servers** to and note the Virtual Server configured to service the SFTP and SSH traffic from the Windows 11 client.

        .. image:: ./images/l1-ltm-vs-ssh.png
            :align: center
            :alt: vs proxy ssh

        We can see that there is a Virtual Server that matches the IP and port used by the SFTP and SSH clients. This means that the traffic from the SFTP and SSH clients are being sent to the BIG-IP system through the SOCKS Proxy virtual server.

In this Lab we looked at how to test the SWG Explicit Forward Proxy configuration using a Windows 11 client. We tested web browsing through the proxy, as well as SFTP and SSH connections using FileZilla and PuTTY, respectively. The next lab will focus on the BIG-IP configuration, specifically working with SWG URL Categories and URL Filters to enforce policies and manage web traffic more effectively.

`Next Lab 2 - SWG URL Categories and Filters <./lab_2_swg_custom_categories.rst>`__

`Main Page <./readme.md>`__