Lab Environment
===============

The lab environment for the F5 Secure Web Gateway Explicit Forward Proxy with Kerberos Lab consists of several components designed to simulate a real-world enterprise environment. The key components include:

The Lab environment includes the following components:  

    - **Windows 2019 Server Active Directory Domain Controller**  
    - **Windows 11 Domain Joined Client**  
    - **BIG-IP SSLO-1**
    - **BIG-IP SSLO-2**

Accessing the Windows machines can be done through the Remote Desktop Protocol (RDP) using the credentials provided in the lab documentation.
Accessing the BIG-IPs will primarily be done through the web-based Traffic Management User Interface (TMUI) using the credentials provided in the lab documentation.

Starting up the Lab in the Course:
----------------------------------
#. Lab participants will receive an UDF course invitation email with details about the course date and time as well as login and account instructions.

    Clicking the links will prompt you to login, if you new to the UDF experience, follow the instructions to create an account with f5.com.

    **Note** The 2nd link will take you directly to the course page.

    .. image:: ./images/udf-coursepage.png
        :align: center
        :alt: udf-coursepage

#. Once on the course page, click the "Join" button to access the lab environment.

#. In the Lab environment you see a Documentation tab and a Deployment tab.

    View the Documentation tab for specific instructions.

    .. image:: ./images/udf-coursedoc.png
        :align: center
        :alt: udf-course-documentation

#. Click the Deployment tab and view the components of the lab. Each of the components will be in the process of starting up. This is indicated by the yellow gear spinning.

    .. image:: ./images/udf-deployment.png
        :align: center
        :alt: udf-deployment

    Allow the environment to fully start up before proceeding to the next step. As the components are staring you can view details about them.

    **Important** Specifically for this lab, the Windows 11 Client is not automatically started. You will manually start it once the AD Server is completely up.

    .. image:: ./images/udf-comp-up.png
        :align: center
        :alt: udf-deployment

#. Log into the BIG-IP by selecting TMUI under the ACCESS menu for BIG-IP SSLO-1 in Deployment.

    .. image:: ./images/udf-bigip-tmui.png
        :align: center
        :alt: tmui

#. Enter the admin username and password.

    .. image:: ./images/l2-bigip-login.png
        :align: center
        :alt: bigip-login



`Next <./lab_1_swg_testing.rst>`__