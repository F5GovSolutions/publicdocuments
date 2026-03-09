Lab 5 - SWG Configurations
==========================

There are several components that are already configured like networking, DNS, NTP.  
Licensing. Outside the scope of these instructions.
SSL Certificates Root Certificates and subordinate certificates that allow the BIG-IP to re-create certificates to establish the connections. These instructions assume that the student has experience with the basics of PKI certificate and key management.

Kerberos is already setup from the Active Directory server with a KeyTab file loaded on to the BIG-IP.

You see some of these elements referred.

(SSLO Configuration)

Task 1 - Create a Custom URL Filter
-----------------------------------

    #. Navigate to **Access > Secure Web Gateway > URL Filters**.

        .. image:: ./images/l-swg-conf-urlfilter-create.png    
            :align: center
            :alt: URL Filters

    #. Click the **Create** button to create a new URL Filter.

    #. On the **General Properties** page give a name to the URL    Filter; for example **"swg_poc_custom"**. Then click **Finished** to create the URL Filter and display the **Properties** page, which shows that the filter has inherited the default filter settings which we will modify in the next steps.

        .. image:: ./images/l-swg-conf-urlfilter-custom.png    
            :align: center
            :alt: Create URL Filter

    #. In the **Associated Categories** list, scroll down to **Sports** and click the box to the left of it to select it. Then click **Block** at the bottom of the page. We will modify the default URL filter to block all URLs categorized under the built-in category of Sports. This is just an example to show how to modify the URL filter settings in our Custom URL Filter. Note the Green Arrow turns into a Red X to indicate that this category is now blocked.

        .. image:: ./images/l-swg-conf-urlfilter-sports.png    
            :align: center
            :alt: Modify URL Filter 

    #. Click the **Update** button in the **General Properties** section to save the changes to our custom URL filter.

    We have now created a custom URL filter and modified it to block all URLs categorized under the built-in category of Sports. In the next steps, we will create a Per Request Policy and use this URL filter in the policy logic.

Task 2 - Per Request Policy Configuration
-----------------------------------------

    #. Navigate to **Access > Profiles / Policies > Per Request Policies**.

        .. image:: ./images/l-swg-conf-prp-create.png
            :align: center
            :alt: Create Per Request Policy

    #. Click the **Create** button to create a new Per Request Policy.

    #. Name the policy; for example **"swg_poc"**, select **All** for the **Policy Type**, and then click **English (en)** and click the **<<** to move it into the **Accepted Languages**. Click the **Finished** button to create the policy with these settings.

        .. image:: ./images/l-swg-conf-prp.png
            :align: center
            :alt: Per Request Policy


    #. Back on the Per Request Policies listing page, click on the **Edit** link for the policy you just created to open the virtual policy editor.

        .. image:: ./images/l-swg-prp-edit.png
            :align: center
            :alt: Per Request Policy Edit


        The **Virtual Policy Editor** is where you can define the specific rules and actions for this policy.

        .. image:: ./images/l-swg-prp-vpe-main.png
            :align: center
            :alt: VPE Page

    #. In the Virtual Policy Editor, click on the **Add New Macro** button. In the drop-down menu, select **SWG Category Lookup**.

        .. image:: ./images/l-swg-prp-vpe-macro.png
            :align: center
            :alt: VPE Macro

    #. The SWG Category Lookup macro logic will populate the macro window.  Click the **Save** button to add it to the main policy.

        .. image:: ./images/l-swg-prp-vpe-save.png
            :align: center
            :alt: VPE Macro Save

    #. The **Macro SWG Category Lookup** will be display in the Per Request Policy main page. Click the **+** button to the left of it to reveal the macro logic. Then click the **URL Filter Assign** button to open the **Properties** page.

        .. image:: ./images/l-swg-prp-vpe-urlf-assign.png
            :align: center
            :alt: VPE url filter Assign

    #. Click the **URL Filter** dropdown to select the URL filter we created earlier to this SWG Category Lookup macro. Click the **Save** button to save the changes.

        .. image:: ./images/l-swg-prp-vpe-urlf-select.png
            :align: center
            :alt: VPE url filter select

    #. Back on the Per Request Policy main page, between the Start and Allow boxes, click the **(+)** to add a policy item; this will link the SWG Category Lookup macro to the main policy. In the page that opens click the **Macros** tab. Select the SWG Category Lookup radio button, and then click the **Add Item** button to add it to the policy.

        .. image:: ./images/l-swg-prp-vpe-policy-macro-add.png
            :align: center
            :alt: VPE policy macro add
    
    #. This is what the policy should look like with the SWG Category Lookup macro added into the policy. Click the **Close** button exit the Virtual Policy Editor.

        .. image:: ./images/l-swg-prp-vpe-policy-finish.png  
            :align: center
            :alt: VPE policy complete
    
Now that we have the URL filter and Per Request Policy configured, we will need to apply this policy to a SWG Service delivered through the SSLO.

Task 3 - SSLO / SWG Configuration
---------------------------------

    #. Navigate to **SSL Orchestrator > Configuration** to launch the Guided Configuration utility. This utility provides several pre-defined configuration templates for different use cases. 
    
    #. Since this is the first configuration for the SSLO it will present you with a Guided configuration page, For this lab, we will select the **L3 Outbound Explicit Proxy** template to enable Explicit Forward Proxy functionality. 

        .. image:: ./images/l-sslo-gc.png
            :align: center
            :alt: SSLO Configuration

    #. Scroll down to the bottom of the page and click **Next**.

        **NOTE** The SSLO Configuration page may complain about "SSL Orchestrator is not initialized."  Wait about 30 seconds and click **SSL Orchestrator > Configuration** again to refresh the page, go to the bottom click **Next**

    #. On the **Topology Properties** page, give the topology a name; for example, **"swg_poc"**. In the SSL Orchestrator Topology section, select **L3 Explicit Proxy** and then scroll down and click **Save & Next**.

        .. image:: ./images/l-sslo-topology.png
            :align: center
            :alt: SSLO Topology

    #. The next page is **SSL Configurations**. In the **Client-side SSL** section click the pencil icon to edit the settings for **Certificate Key Chains**. Select the **proxy_f5labs_local** for certificate and key. This certificate is already provisioned on the BIG-IP and is signed by the subordinate CA that is trusted by the Windows 11 client. This will allow the BIG-IP to re-create certificates for any HTTPS sites visited by the client to allow for SSL inspection and SWG filtering.

        .. image:: ./images/l-sslo-ssl-conf-1.png
            :align: center
            :alt: SSLO SSL Config

    #. In the **CA Certificate Key Chain** section, click the pencil icon to edit the settings. Select the **F5Labs_SubCA_ForwardProxy** certificate and key. This is the subordinate CA certificate that is used to sign the re-created certificates for the HTTPS sites visited by the client.

        .. image:: ./images/l-sslo-ssl-conf-2.png
            :align: center
            :alt: SSLO SSL Config CA
    
    #. Keep everything else default and make sure that the **Trusted Certificate Authority** is set to **ca-bundle.crt**. This will ensure that the BIG-IP trusts the same public CAs as the Windows 11 client for SSL inspection of external sites. Click **Save & Next** to continue.

    #. On the **Authentication List** page, press the **Save & Next** button to continue.

    #. On the **Services List** page, click the **Add Service** button to add a new service.

        .. image:: ./images/l-sslo-service-add.png
            :align: center
            :alt: SSLO Add Service

    #. In the **Service Properties** page, select the **F5** tab and double-click on the **F5 Secure Web Gateway** tile to open it's properties page.

        .. image:: ./images/l-sslo-service-add-f5.png
            :align: center
            :alt: SSLO Add Service F5 SWG

    #. In the **F5 Secure Web Gateway Service properties** page, for **Named Scope** type **"none"**. For the Per Request Policy, select the policy we created earlier; **"swg_poc"**. Then click the **Save** button to save the settings for this service.

        .. image:: ./images/l-sslo-service-add-f5-prp.png
            :align: center
            :alt: SSLO Add Service F5 SWG PRP

    #. The service will now appear in the list of services for this topology configuration. Scroll to the bottom and click the **Save & Next** button to continue.

    #. In the Services Chain List page, click the **Add** button to add the SWG service we just created into the service chain. Give this service chain a name; for example, **"swg_poc"** and then select the SWG service we created from the **Services Available** list and click the **>** button to move it into the **Selected Services Chain Order**. Then click the **Save** button to save the service chain. 

        .. image:: ./images/l-sslo-service-chain-conf.png
            :align: center
            :alt: SSLO Service Chain

    #. In the **Security Policy** page, click the **Save & Next** button to continue.

    #. In the **Interception Rule** page, specify the IPV4 address, we will use 10.1.10.30 for this lab. Select **f5-aws-dns** the DNS Resolver. Then under VLANs, select Client-vlan and the out-vlan, and click the **>** button to move them into the **Selected** list. Leave everything else default and scroll down and click the **Save & Next** button to continue.

        .. image:: ./images/l-sslo-interception-rule.png
            :align: center
            :alt: SSLO Interception Rule

    #. In the **Egress Settings** page, select **Auto Map** for Manage SNAT Settings.  Then click the **Save & Next** button to continue.

    #. In the **Log Settings** page, accept the defaults and click the **Save & Next** button to continue.

    #. In the **Summary** page, there will be a list of all the settings configured for this topology. You have the opportunity to review the settings and if everything looks good, click the **Deploy** button to deploy the configuration.

        .. image:: ./images/l-sslo-summary.png
            :align: center
            :alt: SSLO Summary

    #. When the deployment is complete, you will see a message that says **Deployment was successfully completed**.

        .. image:: ./images/l-sslo-deploy.png
            :align: center
            :alt: SSLO Deploy


`Next Lab 5 - Manage Custom Categories using the iControl Rest API <./lab_5_icontrol_rest_api.rst>`__

`Main Page <./readme.md>`__