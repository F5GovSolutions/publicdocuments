Lab 2 - SWG URL Categories and Filters
========================================

**F5 BIG-IP SWG URL Categories and URL Filters**

URL Categories and URL Filters are core elements of the Secure Web Gateway (SWG) configuration in the Access Policy Manager (APM).

- **URL Categories** represent predefined or custom classifications of web content based on the nature of websites (e.g., News, Social Media, Gambling, Malware, etc.). These categories enable administrators to group similar types of web traffic for easy management.

- **URL Filters** defines policies based on these URL Categories to allow, block, or confirm access to specific types of web content. Filters rules can be configured per request or per user group to enforce corporate browsing policies, extend security, and minimize misuse of network resources.

The SWG relies on the **URL Categories Database** provided by **Forcepoint**, which contains up-to-date information on known websites and their associated categories. This database is downloaded and updated regularly, ensuring that the SWG can effectively classify and filter web traffic. These updates require an active subscription.

In the context of BIG-IP's **Access Policy Manager (APM)**, URL Filtering is integrated into the access policy flow. The user's web requests are evaluated against the URL Categories and Filters during the enforcement of SWG-based policies. When a user sends a web request, the SWG matches the request against the configured URL Categories and applies the corresponding Filters action.

The SWG uses these categories and filters to provide granular control over web access. For example:

- Preventing access to harmful or non-business-related content.
- Logging traffic access for auditing purposes.

Task 1. Working with SWG URL Categories
---------------------------------------

    #. Login to the **BIG-IP SSLO-1 TMUI** (refer to the `Lab Environment <./lab_environment.rst>`)

    #. In the left hand navigation pane select **Access > Secure Web Gateway > URL Categories**.

        A list of URL Categories will appear in the main window, with **Custom Categories** at the top.

    #. Click on the **\'+\'** sign next to **Custom Categories** to expand the list. This reveals that there are 3 custom categories already configured here here.

    #. Select **custom-allow-category** and view the URLs already added to this list.

        .. image:: ./images/l2-bigip-swg-custallcat.png
            :align: center
            :alt: custom-allow-category

    #.  In order to return to the list of URL Categories, click the **Secure Web Gateway : URL Categories** link right above **Properties** in the horizontal navigation bar.

    #.  Expand the Custom Categories again and select **custom-block-category** and view the URLs already added to this list.

        .. image:: ./images/l2-bigip-swg-custblkcat.png
            :align: center
            :alt: custom-block-category
        
        There is only one URL in this category, currently only as a placeholder.

        **Glob Pattern Match**

        The **Glob Pattern Match** setting in URL Categories allows you to define custom URL patterns using wildcards for flexible and precise matching. In this context, "glob" refers to a pattern-matching syntax where you can use special characters like `*` and `?` to specify a range of URLs without listing them individually. For example:

            - '*.example.com' matches all subdomains of 'example.com' (e.g., 'www.example.com', 'blog.example.com').

            - 'example.com/*' matches all paths under 'example.com' (e.g., 'example.com/home', 'example.com/about').

            - 'file?.example.com' matches any single-character variation of 'file' (e.g., 'file1.example.com', 'file2.example.com').

            This setting is useful when you want to create custom URL categories that group related websites or pages based on specific patterns. It provides greater flexibility for administrators to match complex or dynamic site structures that may not be covered by predefined categories.

            Unchecking the Glob setting would require you to specify exact URLs without the use of wildcards.

    #. Return to the list of URL Categories and select **custom-allow-category** again.

        **WARNING:** For this next step there are 2 Delete buttons on this configuration page. Press the one under the Associated URLs list box to delete the chosen URL.

    #. Select the **chatgpt** entry and click the **Delete** button. Then press the **Update** button to save the change.

        This will remove the chatgpt entry from the custom-allow-category list. 
        
        **NOTE:** Removing this entry will cause any requests to chatgpt.com to be categorized according to other URL Categories and Filters configured in the SWG. Depending on the filtering rules, this may result in different handling of requests to chatgpt.com.

        .. image:: ./images/l2-bigip-swg-chatgpt-deleted.png
            :align: center
            :alt: chatgpt-deleted

    #. Return to the list of URL Categories and select **custom-block-category** again.

    #. In the custom-block-category, enter the same chatgpt entry that was just deleted from the custom-allow-category list, **https://*chatgpt.com/**, ensure the **Glob Pattern Match** box is checked.

    #. Now click the **Add** button. Note the entry has been added, then click the **Update** button to save the change.

        This will add the chatgpt entry to the list. 

        .. image:: ./images/l2-bigip-swg-chatgpt-add-blocked.png
            :align: center
            :alt: chatgpt-added

        By adding this entry to the custom-block-category, any requests to chatgpt.com will now be categorized under this block category.

    #. 

    #. Return to the Windows 11 client and open a web browser Chrome or Firefox. Click on the Chatgpt bookmark in the Favorites Bar.

        The request to chatgpt.com should now be blocked by the SWG, and you should see a block page indicating that access to the site has been denied.

        The block page will show you several pieces of information, including the reason for the block (Access Per Request Policy), the session id or reference number, and the category it was categorized under (custom-block-category).

        Even if Chatgpt is categorized under other categories as well, any custom category and filter will take precedence and the request will be blocked.

        .. image:: ./images/l2-bigip-swg-chatgpt-blocked.png
            :align: center
            :alt: chatgpt-page-blocked

Task 3. Working with SWG URL Filters
------------------------------------

    **Understanding URL Filters**

    In the previous steps, you worked with two custom URL Categories: **`custom-allow-category`** and **`custom-block-category`**. While it might seem that placing URLs in these categories directly specifies whether they are allowed or blocked, this is not entirely the case. 

    The actual allow or block decisions are determined by **URL Filters**, not by the URL Categories alone. The custom categories, despite their names and default actions (e.g., Allow or Block), are just groupings of URLs. These categories are referenced in URL Filters, which define the precise actions to take—whether to allow, block, or confirm access. 

    For example, when you added the URL to the **`custom-block-category`**, a URL Filter configured to block that category enforced the action and blocked access. Similarly, when the URL was removed from the **`custom-allow-category`**, the filter no longer allowed access, defaulting to another policy.

    Next, we will take a closer look at **URL Filters**, where the actual policies are applied. This is where you will define how traffic should be treated based on the categories and the rules you configure.

    #. Return to the TMUI and in the left hand navigation pane select **Access > Secure Web Gateway > URL Filters**.

        .. image:: ./images/l2-bigip-swg-urlfilters.png
            :align: center
            :alt: url-filters

    #. Click on **swg-poc-custom** in list of URL Filters to view the filter rules. Then click the **+** next to Custom Categories to expand the list of categories used in this filter.

        The **swg-poc-custom** URL Filter is configured to reference the custom categories you have been working with.

        This URL Filter is configured to block any URLs categorized under `custom-block-category` and allow any URLs categorized under `custom-allow-category`. This is indicated by the Red X for Block and Green Arrow for Allow in the Filtering Action column.

        You can change the filtering action for each category or subcategory by selecting the items on the left column and then scrolling all the way to the bottom and selecting the desired action.

        .. image:: ./images/l2-bigip-swg-urlfilter-rules.png
            :align: center
            :alt: url-filter-rules

`Next Lab 3 - SWG Monitoring and Logs <./lab_3_swg_monitoring_and_logs.rst>`__

`Main Page <./readme.md>`__