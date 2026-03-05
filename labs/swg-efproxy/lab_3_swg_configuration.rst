Lab 3 - SWG Configurations
==========================

There are several components that are already configured like networking, DNS, NTP.  
Licensing. Outside the scope of these instructions.
SSL Certificates Root Certificates and subordinate certificates that allow the BIG-IP to re-create certificates to establish the connections. These instructions assume that the student has experience with the basics of PKI certificate and key management.

Kerberos is already setup from the Active Directory server with a KeyTab file loaded on to the BIG-IP.

You see some of these elements referred.

(SSLO Configuration)

Task 1 - Per Request Policy Configuration
-----------------------------------------

    #. Access > Secure Web Gateway > URL Filters.

        .. image:: ./images/l-swg-conf-urlfilter-create.png    
            :align: center
            :alt: URL Filters

    #. Click the **Create** button to create a new URL Filter.

    #. On the **General Properties** page give a name to the URL Filter; for example **"swg_poc_custom"**. Then click **Finished** to create the URL Filter. This filter will inherit the default filter settings which we will modify in the next steps.

        .. image:: ./images/l-swg-conf-urlfilter-custom.png    
            :align: center
            :alt: Create URL Filter

    #. In the **Associated Categories** list, scroll down to **Sports** and click the box to the left of it to select it. Then click **Block** at the bottom of the page. We will modify the default URL filter to block all URLs categorized under the built-in category of Sports. This is just an example to show how to modify the URL filter settings. In a production environment you would likely want to block categories that are more risky such as Gambling or Malicious Sites.

        .. image:: ./images/l-swg-conf-urlfilter-sports.png    
            :align: center
            :alt: Modify URL Filter 

    #. Click the **Update** button in the **General Properties** section to save the changes to our custom URL filter.

    #. Access > Profiles / Policies > Per Reqeust Policies.

        .. image:: ./images/l-swg-conf-prp.png
            :align: center
            :alt: Per Request Policy

    #. Click the **Create** button to create a new Per Request Policy.

    #. Name the policy; for example **"swg_poc"**, select **All** for the **Policy Type**, and then click **English (en)** and click the **<<** to move it into the **Accepted Languages**. Click the **Finished** button to create the policy with these settings.

        .. image:: ./images/l-swg-conf-prp-create.png
            :align: center
            :alt: Create Per Request Policy

    #. Back on the Per Request Policies listing page, click on the **Edit** link for the policy you just created to open the policy editor.

        .. image:: ./images/l-swg-prp-edit.png
            :align: center
            :alt: Per Request Policy Edit


        This will open the Virtual Policy Editor where you can define the rules and actions for this policy.

        .. image:: ./images/l-swg-prp-vpe-main.png
            :align: center
            :alt: VPE Page

    #. In the Virtual Policy Editor, click on the **Add New Macro** button. In the drop-down menu, select **SWG Category Lookup**.

        .. image:: ./images/l-swg-prp-vpe-macro.png
            :align: center
            :alt: VPE Macro

    #. The SWG Category Lookup macro logic will populate the main window.  Click the **Save** button to add it to the policy.

        .. image:: ./images/l-swg-prp-vpe-save.png
            :align: center
            :alt: VPE Macro Save

    #. The **Macro SWG Category Lookup** will be display in the Per Request Policy.  Press the **+** button to reveal the macro logic. Click the **URL Filter Assign** button to open the **Properties** page.

        .. image:: ./images/l-swg-prp-vpe-urlf-assign.png
            :align: center
            :alt: VPE url filter Assign

    #. Click the **URL Filter** dropdown to select the URL filter we created earlier to this SWG Category Lookup macro. Click the **Save** button to save the changes.

        .. image:: ./images/l-swg-prp-vpe-urlf-select.png
            :align: center
            :alt: VPE url filter select

    #. Back on the Per Policy, between the Start and Allow click the **+** to add a policy item; this will link the SWG Category Lookup macro to the main policy. In the page that opens click the **Macro** tab. Select the SWG Category Lookup radio button, and then click the **Add Item** button to add it to the policy.

        .. image:: ./images/l-swg-prp-vpe-policy-macro-add.png
            :align: center
            :alt: VPE policy macro add
    
    #. This is what the policy should look like with the SWG Category Lookup macro added to it. Click the **Close** button exit the Virtual Policy Editor.

        .. image:: ./images/l-swg-prp-vpe-policy-finish.png  
            :align: center
            :alt: VPE policy complete
    
Now that we have the URL filter and Per Request Policy configured, we will need to apply this policy to a SWG Service delivery through the SSLO.

Task 2 - SWG / SSLO Configuration
---------------------------



**URL Categories and URL Filters in F5 BIG-IP SWG**



`Next Lab 4 - Manage Custom Categories using the CLI <./lab_4_swg_manage_cli.rst>`__

`Main Page <./readme.md>`__