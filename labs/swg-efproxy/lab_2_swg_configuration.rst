Lab 2 Instructions for SWG Explict Forward Proxy

Task 1. Review the SWG URL Categories and URL Filtering

#. Log into the BIG-IP by selecting TMUI under the ACCESS menu for BIG-IP SSLO-1 in Deployment.

    .. image:: ./images/l2-bigip-tmui.png
        :align: center
        :alt: tmui

#. Enter the admin username and password.

    .. image:: ./images/l2-bigip-login.png
        :align: center
        :alt: bigip-login

#. In the left hand navigation pane select Access > Secure Web Gateway > URL Categories.

A list of URL Categories will appear in the main window, with Custom Categories at the top.

#. Click on the '+' sign next to **Custom Categories** to expand the list. This reveals that there are 3 custom categories already configured here here.

#.  Select "custom-allow-category" and view the URLs already added to this list.

![custom-allow-category](./images/l2-bigip-swg-custallcat.png)
    .. image:: ./images/l2-bigip-swg-custblkcat.png
        :align: center
        :alt: custom-allow-category

#.  Return to the list of URL Categories by clicking **Secure Web Gateway : URL Categories** link right above **Properties** in the navigation bar.

#.  Expand the Custom Categories again and select "custom-block-category" and view the URLs already added to this list.

    .. image:: ./images/l2-bigip-swg-custblkcat.png
        :align: center
        :alt: custom-block-category