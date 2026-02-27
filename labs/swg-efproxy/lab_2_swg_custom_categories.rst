Lab 2 - SWG URL Categories and Filters
========================================

**URL Categories and URL Filters in F5 BIG-IP SWG**

URL Categories and URL Filters are core elements of the Secure Web Gateway (SWG) configuration in the Access Policy Manager (APM).

- **URL Categories** represent predefined or custom classifications of web content based on the nature of websites (e.g., News, Social Media, Gambling, Malware, etc.). These categories enable administrators to group similar types of web traffic for easy management.

- **URL Filters** defines policies based on these URL Categories to allow, block, or confirm access to specific types of web content. Filters rules can be configured per request or per user group to enforce corporate browsing policies, extend security, and minimize misuse of network resources.

The SWG relies on the **URL Categories Database** provided by **Forcepoint**, which contains up-to-date information on known websites and their associated categories. This database is downloaded and updated regularly, ensuring that the SWG can effectively classify and filter web traffic. These updates require an active subscription.

In the context of an **APM Policy**, URL Filtering is integrated into the access policy flow. The user's web requests are evaluated against the URL Categories and Filters during the enforcement of SWG-based policies. When a user sends a web request, the SWG matches the request against the configured URL Categories and applies the corresponding Filters action.

The SWG uses these categories and filters to provide granular control over web access. For example:

- Preventing access to harmful or non-business-related content.
- Logging traffic access for auditing purposes.
- Dynamically adjusting resources based on user entitlements or policies.

By linking URL Categories, URL Filters rules, and APM policies, the SWG ensures both secure and policy-compliant web access for users in the network.

**Task 0. Managing Client Sessions and Browser Behavior in the Lab**

    When working in this lab environment, there will be times when you need to "kill" client sessions. This is especially important when making changes to URL Categories or URL Filters, as active sessions still use cached policy information. By clearing the session, any updates to the policy configurations are applied on the next request.

    In this lab, the per-session timeout is set to the default of 5 minutes. However, waiting for the session to age out naturally can slow down your testing workflow. To avoid delays:

    - You will manually 'kill' sessions from the BIG-IP.
    - After clearing the session, the client will establish a new session with the updated settings.

    **Important: Close All Browsers on the Client**

    It's critical to close all web browsers running on the client, as browsers and websites often maintain constant background communication with the internet. This chatter can unintentionally create new sessions or interfere with the changes you are testing.

    **Steps to Ensure Clean Testing:**

#.  Fully close all web browsers on the client machine to stop background traffic.

#.  On the TMUI Select Access > Overview > Active Sessions to view all active sessions.

    .. image:: ./images/l2-bigip-apm-activesess.png
        :align: center
        :alt: active-sessions

#.  Set the Auto Refresh to 10 seconds to make it easier to see new sessions as they are created.

    .. image:: ./images/l2-bigip-apm-killsession.png
        :align: center
        :alt: kill-session

#.  Select the session(s) associated with the client machine; there should only be one session associated with the client machine, and then click the "Kill Selected Session" button.

#.  On the Confirm Delete page, click the "Delete" button to confirm the session termination.

     This will immediately terminate the selected session(s).

     **Note**: After killing the session, any new web requests from the client will establish a new session that reflects the latest policy configurations. This ensures that your testing of URL Categories and Filters is accurate.

    .. image:: ./images/l2-bigip-apm-killsession-confirm.png
        :align: center
        :alt: kill-session

#.  After making changes described in the following tasks, you must follow these steps to start a new session to reflect any changes or updates to the URL Categories or URL Filters.

**Task 1. Working with SWG URL Categories**

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
    
    There is only one URL in this category, currently only as a placeholder. A custom category needs at least one URL to be defined.

    **Glob Setting in URL Categories**

    The Glob setting in URL Categories allows you to define custom URL patterns using wildcards for flexible and precise matching. In this context, "glob" refers to a pattern-matching syntax where you can use special characters like `*` and `?` to specify a range of URLs without listing them individually. For example:

        - `*.example.com` matches all subdomains of `example.com` (e.g., `www.example.com`, `blog.example.com`).

        - `example.com/*` matches all paths under `example.com` (e.g., `example.com/home`, `example.com/about`).

        - `file?.example.com` matches any single-character variation of `file` (e.g., `file1.example.com`, `file2.example.com`).

        This setting is useful when you want to create custom URL categories that group related websites or pages based on specific patterns. It provides greater flexibility for administrators to match complex or dynamic site structures that may not be covered by predefined categories.

        Unchecking the Glob setting would require you to specify exact URLs without the use of wildcards.

#. Return to the list of URL Categories and select "custom-allow-category" again.

    Take note of the chatgpt entry;  **https://*chatgpt.com/**

#.  Select the chatgpt entry and click the Delete button. Then press the Update button to save the change.

    This will remove the chatgpt entry from the custom-allow-category list. 

    **.. warning:: There are 2 Delete buttons on this configuration page. Press the one under the Associated URLs list box to delete the chosen URL.
    
    **Note**: Removing this entry will cause any requests to chatgpt.com to be categorized according to other URL Categories and Filters configured in the SWG. Depending on the filtering rules, this may result in blocked access or different handling of requests to chatgpt.com.

    .. image:: ./images/l2-bigip-swg-chatgpt-deleted.png
        :align: center
        :alt: chatgpt-deleted

#. Return to the list of URL Categories and select "custom-block-category" again.

#. In the custom-block-category, enter the same chatgpt entry that was just deleted from the custom-allow-category list, **https://*chatgpt.com/**, ensure the Glob Pattern Match box is checked.

#. Now click the Add button. Note the entry has been added, then click the Update button to save the change.

    This will add the chatgpt entry to the custom-block-category list. 

    .. image:: ./images/l2-bigip-swg-chatgpt-add-blocked.png
        :align: center
        :alt: chatgpt-added

    By adding this entry to the custom-block-category, any requests to chatgpt.com will now be categorized under this block category.

#. Return to the Windows 11 client and open a web browser Chrome or Firefox. Click on the Chatgpt bookmark in the Favorites Bar.

    The request to chatgpt.com should now be blocked by the SWG, and you should see a block page indicating that access to the site has been denied.

    The block page will show you several pieces of information, including the reason for the block (Access Per Request Policy), the session id or reference number, and the category it was categorized under (custom-block-category).

    Even if Chatgpt is categorized under other categories as well, any custom category and filter will take precedence and the request will be blocked.

    .. image:: ./images/l2-bigip-swg-chatgpt-blocked.png
        :align: center
        :alt: chatgpt-page-blocked

**Task 2. Clearing Sessions**




**Task 2. Working with URL Filters**

    **Understanding Custom URL Categories and URL Filters**

    In the previous steps, you worked with two custom URL Categories: `custom-allow-category` and `custom-block-category`. While it might seem that placing URLs in these categories directly specifies whether they are allowed or blocked, this is not entirely the case. 

    The actual allow or block decisions are determined by **URL Filters**, not by the URL Categories alone. The custom categories, despite their names and default actions (e.g., Allow or Block), are just groupings of URLs. These categories are referenced in URL Filters, which define the precise actions to take—whether to allow, block, or confirm access. 

    For example, when you added the URL to the `custom-block-category`, a URL Filter configured to block that category enforced the action and blocked access. Similarly, when the URL was removed from the `custom-allow-category`, the filter no longer allowed access, defaulting to another policy.

    Next, we will take a closer look at **URL Filters**, where the actual policies are applied. This is where you will define how traffic should be treated based on the categories and the rules you configure.

#. Return to the TMUI and in the left hand navigation pane select Access > Secure Web Gateway > URL Filters.

    .. image:: ./images/l2-bigip-swg-urlfilters.png
        :align: center
        :alt: url-filters

#. Click on "swg-poc-custom" in list of URL Filters to view the filter rules. Then click the + next to Custom Categories to expand the list of categories used in this filter.

    The "swg-poc-custom" URL Filter is configured to reference the custom categories you have been working with.

    This URL Filter is configured to block any URLs categorized under `custom-block-category` and allow any URLs categorized under `custom-allow-category`. This is ind by the Red X for Block and Green Arrow for Allow in the Filtering Action column.

    You can change the filtering action for each category or subcategory by selecting the items on the left column and then scrolling all the way to the bottom and selecting the desired action.

    .. image:: ./images/l2-bigip-swg-urlfilter-rules.png
        :align: center
        :alt: url-filter-rules

