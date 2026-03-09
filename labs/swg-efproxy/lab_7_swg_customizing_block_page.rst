Lab 7 - Customizing the URL Filtering Block Page
================================================

In this lab, you will customize the URL filtering block page that is displayed to users when they attempt to access a URL that has been blocked by the SWG. This will allow you to provide a more informative and branded experience for users who encounter blocked content.

https://techdocs.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-customization-12-0-0/2.html#unique_771735672


Task 1. Accessing the Block Page Customization Settings
------------------------------------------------------- 

    #. Log in to the BIG-IP Configuration Utility and navigate to **Access > Profiles / Policies > Customization > General**.

        .. image:: ./images/l6-apm-custom-general.png
            :align: center
            :alt: Customizations

        You will see a list of BIG-IP objects that can be customized, including Per Request Policies, Access Profiles, and more. For this lab, we will focus on customizing the block page for URL filtering, which falls under the Per Request Policy customization.

    #. Click on the **Per Request Policy** to expand it, then click the Per Request Policy we created previously; in this example **swg-poc**. Under the policy click on the **Common** folder which contain the customizeable objects.

        .. image:: ./images/l6-apm-custom-prp.png
            :align: center
            :alt: Per Request Policy Customization

    #. In the configuration area, there is a left navigation pane as well as another pane for the making the customization edits.

        Let's review the block page we've been receiving.

        .. image:: ./images/l6-apm-custom-elemnts.png
            :align: center
            :alt: block page elements

        The logo is in the header of the page. Logos are can be changed through the **Branding** configuration tab. The text elements; those in the body and the footer are customized in the **Text** configuration tab.

    #. In the left nav pane let's select **Text** first. 

    #. On the WebShell of BIG-IP SSLO-1 issue the command:: 

# This is the End of the Lab.