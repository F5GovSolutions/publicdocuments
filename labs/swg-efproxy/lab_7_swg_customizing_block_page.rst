Lab 7 - Customizing the URL Filtering Block Page
================================================

In this lab, you will customize the Access Policy block page that is displayed to users when they attempt to access a URL that has been blocked by the SWG. This will allow you to provide a more informative and branded experience for users who encounter blocked content.

**REFERENCE:**
https://techdocs.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-customization-12-0-0/2.html#unique_771735672


Task 1. Accessing the Block Page Customization Settings
------------------------------------------------------- 

    #. Log in to the BIG-IP Configuration Utility and navigate to **Access > Profiles / Policies > Customization > General**.

        .. image:: ./images/l7-apm-custom-general.png
            :align: center
            :alt: Customizations

        You will see a list of BIG-IP objects that can be customized, including *Per Request Policies*, Access Profiles, and more. For this lab, we will focus on customizing the block page for URL filtering, which falls under the Per Request Policy customization.

    #. Click on the **Per Request Policy** folder to expand it, then click the Per Request Policy we are working with; in this example **swg-poc**. Under the policy click on the **Common** folder which contain the customizeable objects.

        Let's review the block page we've been receiving.

        .. image:: ./images/l7-apm-custom-elemnts.png
            :align: center
            :alt: block page elements

        The logo is in the header of the page. Logos are can be changed through the **Branding** configuration tab. The text elements; those in the body and the footer are customized in the **Text** configuration tab.

    #. Notice in the left navigation pane there is a **Branding** tab and a **Text** tab. Select **Branding** tab first.

    #. Then in the **Per Request Policy > Common/swg_poc > Common** folder select **Header, Footer, Title** in the list. This reveals the Header Image For Desktop and Mobile. 

        .. image:: ./images/l7-apm-custom-logo.png
            :align: center
            :alt: logo value    

    #. Click the entry in the Value column for the Header Image for Desktop. This will open a dialog box showing the current logo. Click the Replace button to open the Choose an Image where you can select an image that was previously uploaded to the BIG-IP. 

        .. image:: ./images/l7-apm-custom-choose.png
            :align: center
            :alt: logo choose  

    #. Click on one of the images, it will reveal the full name of the image. Select the image that has 60px in the name. The logo was created to be 60 pixels in height to fit well in the header of the block page. After selecting the image, click the **Change** button to save.

    #. Up near the top navigation bar, click the **Save** icon button to save the changes to the customization.

        .. image:: ./images/l7-apm-custom-save.png
            :align: center
            :alt: customization save  

    #. Open the **Web Shell** of **BIG-IP SSLO-1**; in the TMSH context, issue the command; 

        tmsh:: 
            delete ltm profile ramcache all

        **NOTE:** There is no output from this command.
        
        This will clear the RAM cache profile, which is used to cache block pages. By clearing the cache, we can ensure that any changes we make to the block page will be reflected immediately when we test it.

    #. Return to the Windows 11 client and open a web browser and attempt to access a blocked URL.

        You should see the default block page with the default text and new logo.

        .. image:: ./images/l7-apm-custom-updated.png
            :align: center
            :alt: logo updated

    **TIP:** Use the Chrome shortcut on the Desktop as it is configured to use Incognito mode, which will clear any locally cached content in the session. Close the browser before making further changes.

Task 2. Customizing the Block Page Text
---------------------------------------

    #. Back in the left navigation pane now choose the **Text** tab.

        Locations of the Text elements on the block page.

            - Text: Access to this page is blocked - Logout > Application and URL filters > URL Filter denied reject message
            - Text: The category reference is: - Logout > Application and URL filters > URL Filter denied page category message
            - Text: Session reference number - Logout > General > Session ID
            - Text: Access was denied by a per-request policy. - Error Messages > General Errors > Access Denied by Per-Request Resource policy

    #. Make changes to the text elements as desired. 
    
        - Remember to click the Save icon near the top navigation bar to save any changes.
        - Remember to issue the TMSH command to clear the RAMCACHE.

    #. Test the block page again by accessing a blocked URL from the Windows client and review the changes you made.

    **TIP:** Use the Chrome shortcut on the Desktop as it is configured to use Incognito mode, which will clear any locally cached content in the session. Close the browser before making further changes.

# This is the End of the Lab.

`Main Page <./readme.md>`__