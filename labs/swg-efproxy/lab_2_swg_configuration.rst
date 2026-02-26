Lab 2 - SWG URL Categories and Filtering
========================================

**URL Categories and URL Filtering in F5 BIG-IP SWG**

URL Categories and URL Filtering are core elements of the Secure Web Gateway (SWG) configuration in the Access Policy Manager (APM).

- **URL Categories** represent predefined or custom classifications of web content based on the nature of websites (e.g., News, Social Media, Gambling, Malware, etc.). These categories enable administrators to group similar types of web traffic for easy management.

- **URL Filtering** defines policies based on these URL Categories to allow, block, or confirm access to specific types of web content. Filtering rules can be configured per request or per user group to enforce corporate browsing policies, extend security, and minimize misuse of network resources.

In the context of an **APM Policy**, URL Filtering is integrated into the access policy flow. The user's web requests are evaluated against the URL Categories and Filters during the enforcement of SWG-based policies. When a user sends a web request, the SWG matches the request against the configured URL Categories and applies the corresponding filtering action.

The SWG uses these categories and filters to provide granular control over web access. For example:

- Preventing access to harmful or non-business-related content.
- Logging traffic access for auditing purposes.
- Dynamically adjusting resources based on user entitlements or policies.

By linking URL Categories, URL Filtering rules, and APM policies, the SWG ensures both secure and policy-compliant web access for users in the network.

**Task 1. Review the SWG URL Categories and URL Filtering**

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

#. Select "custom-allow-category" and view the URLs already added to this list.

    .. image:: ./images/l2-bigip-swg-custallcat.png
        :align: center
        :alt: custom-allow-category

#.  Return to the list of URL Categories by clicking **Secure Web Gateway : URL Categories** link right above **Properties** in the navigation bar.

#.  Expand the Custom Categories again and select "custom-block-category" and view the URLs already added to this list.

    .. image:: ./images/l2-bigip-swg-custblkcat.png
        :align: center
        :alt: custom-block-category