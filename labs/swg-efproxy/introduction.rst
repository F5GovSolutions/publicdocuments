F5 Secure Web Gateway Explicit Forward Proxy with Kerberos Lab
==============================================================

**Purpose:**

The purpose of this Lab is to become familiar with the F5 Secure Web Gateway (SWG) Forward Proxy management and configuration.

The Lab environment includes several components:  

- An **Active Directory Domain Controller** for user authentication,  
- A **Windows 11 Client PC** to simulate user interactions,  
- Two **BIG-IP VE** (Virtual Edition) instances to provide proxy services.

  - BIG-IP SSLO-1 fully configured as the SWG Explicit Forward Proxy.

  - BIG-IP SSLO-2 minimally configured.

- Several interconnected networks to simulate real-world environments.

The Lab leverages **Kerberos authentication**, configured on the BIGIP-SSLO-1, to authenticate users via an **Access Policy Manager (APM)** policy. The authentication enables logging of user URL requests.

**Background on SWG and SSLO**

The **Secure Web Gateway (SWG)** is a service component of the BIG-IP platform that combines web filtering and categorization of web traffic. As part of the **SSL Orchestrator (SSLO)** Services catalog, the SWG can play an integral role in managing secure Zero Trust environments.

**General Tasks**

    - Test the SWG's functionality from a client workstation, and view its proxy configuration from the client perspective.
    - Manage SWG's **custom category configurations**, including modification of default categories and creation of custom ones.
    - Configure and manage **URL filtering policies** to enforce compliance and block specific content types or categories.
    - Monitor and analyze **SWG logging outputs** to track, troubleshoot, and audit user behaviors and URL requests.

The Lab underscores the SWG's versatility, showing how it combines secure web traffic filtering with robust traffic management and user authentication capabilities.

`Next Lab Environment <./lab_environment.rst>`__

`Main Page <./readme.md>`__