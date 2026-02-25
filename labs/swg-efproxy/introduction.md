# F5 Secure Web Gateway Explicit Forward Proxy with Kerberos Labs

### Purpose
The purpose of this Lab is to become familiar with the F5 Secure Web Gateway (SWG) Forward Proxy configuration and operation.  
The Lab environment includes several components:  
- An **Active Directory Domain Controller** for user authentication,  
- A **Windows 11 Client PC** to simulate user interactions,  
- Two **BIG-IP VE** (Virtual Edition) instances to provide proxy and application services, and  
- Several interconnected networks to simulate real-world environments.

The Lab leverages **Kerberos authentication**, configured on the BIGIP-SSLO-1, to authenticate users via an **Access Policy Manager (APM)** policy. This APM policy enables logging of user activities, including URL requests. By the end of this Lab, you'll have hands-on experience with configuring and monitoring the SWG in a secure, enterprise-grade environment.

### Background on SWG and SSLO
The **Secure Web Gateway (SWG)** is a key component of the BIG-IP platform that combines web filtering and access policy management to secure web traffic. As part of the **SSL Orchestrator (SSLO)** Services catalog, the SWG serves as an integral element in managing secure, encrypted environments. 

The SWG's integration with APM adds significant value by enabling granular user authentication, policy enforcement, and detailed logging of user browsing behaviors. This makes it ideal for organizations that require advanced control and oversight over web traffic. 

Additionally, the SWG operates as a part of the **SSL Orchestrator topologies**, offering advanced forward proxy capabilities. These capabilities are essential not only for providing secure content but also for decrypting, inspecting, and re-encrypting traffic in a unified manner. 

This make SWG not just a simple proxy tool, but a **flexible and powerful solution**—scalable to fit the needs of various environments, from basic URL filtering to advanced user and application-level inspection. Its flexibility allows administrators to create custom categories, leverage existing category databases, and enforce compliance at many levels of the network.

### General Tasks
- Test the SWG's functionality from a client workstation, and view its proxy configuration from the client perspective.
- Manage SWG's **custom category configurations**, including modification of default categories and creation of custom ones.
- Configure and manage **URL filtering policies** to enforce compliance and block specific content types or categories.
- Monitor and analyze **SWG logging outputs** to track, troubleshoot, and audit user behaviors and URL requests.

The Lab underscores the SWG's versatility, showing how it combines secure web traffic filtering with robust traffic management and user authentication capabilities.

[Previous Page](./readme.md) | [Next Page](./lab_1_swg_testing.md)