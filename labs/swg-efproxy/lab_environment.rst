Lab Environment
===============

If you are familiar with the UDF lab environment, you can skip to the next section. 

`Lab 1 Testing the SWG Explict Forward Proxy <./lab_1_swg_testing.rst>`__

If you are new to the UDF lab environment, this section will provide an overview of the lab environment and how to access it.

The UDF lab environment for the **F5 Secure Web Gateway Explicit Forward Proxy with Kerberos Lab** consists of several components designed to simulate a real-world enterprise environment. The key components include:

    - **BIG-IP SSLO-1**
    - **BIG-IP SSLO-2**
    - **Windows 2019 Server Active Directory Domain Controller**  
    - **Windows 11 Domain Joined Client**  
  
Accessing the Windows instances can be done through the **Remote Desktop Protocol (RDP)** or the **SuperJump Host** using the credentials provided in the lab documentation.
Accessing the BIG-IPs will primarily be done through the web-based **Traffic Management User Interface (TMUI)** and the **WebShell** for command-line access. Again, the credentials for accessing these components are provided.

Starting up the Lab in the Course:
----------------------------------
#. Lab participants will receive an UDF course invitation email with details about the course date and time as well as login and account instructions.

    Clicking the links will prompt you to login, 
    
    If you new to the UDF experience, follow the instructions to create an account with f5.com.

    **Note** There are 2 links in the e-mail. One will take you to the general course landing page and the other will take you directly to the course.

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

    **Important** Specifically for this lab, the Windows 11 does not start automatically with the rest of the systems; indicated by a red square. You will manually start it after all the other systems are completely up.

    .. image:: ./images/udf-deployment.png
        :align: center
        :alt: udf-deployment

    Allow the environment to fully start up before proceeding to the next step. As the components are staring you can view details about them.

    .. image:: ./images/udf-comp-up.png
        :align: center
        :alt: udf-deployment

#. Press the **Details** button for the Windows 11 instance, then press the **Start** button in the pop-up window to start the instance. Allow the instance to fully start up before proceeding to the next step.

    **Note** Notice the user accounts listed on the Details page. These are the credentials you will use to log into the Windows 11 client instance.

    .. image:: ./images/udf-win11-start.png
        :align: center
        :alt: udf-win11-start

Logging into the Windows 11 Client using the RDP method:
--------------------------------------------------------

#. Press the "Access" button for the Windows 11 Client, and 



Logging into the Windows 11 Client using the SuperJump Host method:
-------------------------------------------------------------------



#. Press the "Access" button on the SuperJump Host.

#. Enter the admin username and password.

    .. image:: ./images/udf-bigip-login.png
        :align: center
        :alt: bigip-login

Logging into the BIG-IP TMUI:
-----------------------------

#. From the ACCESS menu of the BIG-IP select TMUI.

    .. image:: ./images/udf-bigip-tmui.png
        :align: center
        :alt: tmui 

Logging into the BIG-IP WebShell:
---------------------------------

#. From the ACCESS menu of the BIG-IP select WebShell.

    .. image:: ./images/udf-bigip-webshell.png
        :align: center
        :alt: webshell 

`Next Lab 1 Testing the SWG Explict Forward Proxy <./lab_1_swg_testing.rst>`__