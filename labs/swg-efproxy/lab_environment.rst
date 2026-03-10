Lab Environment
===============

If you are familiar with the UDF lab environment, you can skip to the next section. 

`Lab 1 - Testing the SWG Explict Forward Proxy <./lab_1_swg_testing.rst>`__

If you are new to the UDF lab environment, this section will provide an overview of the lab environment and how to access it.

The UDF lab environment for the **F5 Secure Web Gateway Explicit Forward Proxy with Kerberos Lab** consists of several components designed to simulate a real-world enterprise environment. The key components include:

    - **BIG-IP SSLO-1**
    - **BIG-IP SSLO-2**
    - **Windows 2019 Server Active Directory Domain Controller**  
    - **Windows 11 Domain Joined Client**  
  
Accessing the Windows instances can be done through the **Remote Desktop Protocol (RDP)** or the **SuperJump Host** using the credentials provided in the details tab of each component in the deployment.
Accessing the BIG-IPs will primarily be done through the web-based **Traffic Management User Interface (TMUI)** and the **WebShell** for command-line access.

Credentials:
------------
    
    +-----------------+------------+-----------------+
    | Component       | Username   | Password        |
    +=================+============+=================+
    | BIG-IP TMUI     | admin      | f5Twister!      |
    +-----------------+------------+-----------------+
    | Windows 11      | f5guy      | f5Twister!      |
    +-----------------+------------+-----------------+
    | SuperJump Host  | rdpuser    | f5Twister!      |
    +-----------------+------------+-----------------+


Starting up the Lab in the Course:
----------------------------------

    #. Lab participants will receive an UDF course invitation email with details about the course date and time as well as login and account instructions.

        Clicking the links will prompt you to login, 
        
        If you new to the UDF experience, follow the instructions to create an account with f5.com.

        **NOTE:** There are 2 links in the e-mail. One will take you to the general course landing page and the other will take you directly to the course.

        **Important** Select "Invited Users" at the UDF portal landing page.
        
        .. image:: ./images/udf-coursepage.png
            :align: center
            :alt: udf-coursepage

    #. Once on the course page, click the "Join" button to access the lab environment.

    #. In the Lab environment you see a **Documentation** tab and a **Deployment** tab.

        View the Documentation tab for specific instructions.

        .. image:: ./images/udf-coursedoc.png
            :align: center
            :alt: udf-course-documentation

    #. Click the Deployment tab and view the components of the lab. Each of the components will be in the process of starting up. This is indicated by the yellow gear spinning.

        .. image:: ./images/udf-comp-start.png
            :align: center
            :alt: udf-deployment

        Allow the environment to fully start up before proceeding to the next step. As the components are staring you can view details about them.

        .. image:: ./images/udf-comp-up.png
            :align: center
            :alt: udf-deployment

Logging into the Windows 11 Client using the RDP method:
--------------------------------------------------------

    #. From the **Access** menu of the **Windows 11 Client**, and select an RDP resolution. This will download an RDP file to your local machine. Open this file to launch the Remote Desktop Connection application and connect to the Windows 11 client.

    **TIP:** Pick a resolution equal to or smaller than your local machine's screen resolution to ensure the best experience. The RDP app will allow you to into full screen mode or windowed mode once you are connected.

        .. image:: ./images/udf-win11-rdp-resolution.png
            :align: center
            :alt: rdp resolution

    #. Enter username and password to log in found on the **Details** page.. 

        **IMPORTANT:** If you are on a Windows machine, you'll have to enter the Domain\\username (for example: f5labs\\f5guy). If using a Mac, you will only need to enter the username.   

        .. image:: ./images/udf-win11-rdp-win-logon.png
            :align: center
            :alt: win11 logon

        .. image:: ./images/udf-win11-rdp-mac-logon1.png
            :align: center
            :alt: MacOS logon

        **NOTE:** A security warning about trusting the Certificate will pops up,
    
            - If on a Windows machine, click **Yes** to proceed.
            - If on a Mac, click **Continue** to proceed.

    #. Once logged in, you will see the Windows 11 desktop with browsers, FileZilla, and PuTTY pre-installed.

        .. image:: ./images/udf-win11-rdp-desktop.png
            :align: center
            :alt: win11 desktop

Logging into the Windows 11 Client using the SuperJump Host method:
-------------------------------------------------------------------

    #. From the **Access** menu of the SuperJump Host, select **Guacamole**. This will open a new browser tab with the Guacamole login page.

        .. image:: ./images/udf-sjh-guac.png
            :align: center
            :alt: guacamole

    #. Enter the username and password found on the Details page of the SuperJump Host.

        .. image:: ./images/udf-sjh-guac-login.png
            :align: center
            :alt: guacamole-login

    #. Once logged in, under **All Connections** select the **Win11 Domain Joined..._RDP** link.
    
        .. image:: ./images/udf-sjh-connections.png
            :align: center
            :alt: superjump connections

    #. This will open a new tab in your browser with a Remote Desktop session to the Windows 11 client. Use the credentials found on the Details page of the Windows 11 instance to log in.

        .. image:: ./images/udf-sjh-win11-logon.png
            :align: center
            :alt: win11-login

        Once logged in, you will see the Windows 11 desktop with browsers, FileZilla, and PuTTY pre-installed.

        .. image:: ./images/udf-sjh-win11-desktop.png
            :align: center
            :alt: win11 desktop

Logging into the BIG-IP TMUI:
-----------------------------

    #. From the ACCESS menu of the BIG-IP select TMUI.

        .. image:: ./images/udf-bigip-tmui.png
            :align: center
            :alt: tmui 

    #. Enter the username and password provided in the **Details** page.

        .. image:: ./images/udf-bigip-login.png
            :align: center
            :alt: tmui login

Logging into the BIG-IP WebShell:
---------------------------------

    #. From the ACCESS menu of the BIG-IP select WebShell.

        .. image:: ./images/udf-bigip-webshell.png
            :align: center
            :alt: webshell 

    This will open a new browser tab with a command-line interface to the BIG-IP.

Now you are ready to start working through the labs. The next section will cover testing the SWG Explicit Forward Proxy configuration from the Windows 11 client.

`Next Lab 1 - Testing the SWG Explict Forward Proxy <./lab_1_swg_testing.rst>`__

`Main Page <./readme.md>`__