Lab 6 - Manage Custom Categories and Filters using the CLI
==========================================================

Task 0. TMSH and bash Contexts
------------------------------

**Understanding TMSH and Bash CLI Contexts**

In this lab, you will be working directly with the BIG-IP system using both **TMSH** (Traffic Management Shell) and **Bash CLI** contexts. These interfaces provide powerful ways to interact with the system, each serving distinct purposes and offering specific functionality.

- **TMSH (Traffic Management Shell)**: 
  - TMSH is the primary administrative interface for managing and configuring BIG-IP systems. It provides a structured and intuitive way to interact with system objects, configuration settings, and operational data.
  - Using TMSH allows you to make changes to BIG-IP configurations, retrieve statistical data, and interact with the system in a controlled manner. It is directly tied to the BIG-IP management framework and ensures safety and consistent behavior within the system.

    When you are in the TMSH context the prompt will look like this::

        root@(bigip1)(cfg-sync Standalone)(TimeLimitedModules::Active)(/Common)(tmos)# 

    **NOTE** The **(tmos)** at the end of the prompt is simplist indication that you are in the TMSH context.

- **Bash CLI**:
  - Bash CLI provides direct access to the underlying operating system of the BIG-IP system. It is more low-level and powerful, enabling you to manage files, troubleshoot issues, and run advanced administrative commands.
  - While Bash CLI offers flexibility, it also requires caution as improper commands can impact the system’s functionality or stability.

    The prompt in the Bash CLI context will look like this::

        root@bigip1:TimeLimitedModules::Active:Standalone] config #

**Important: Be Careful with Commands**

When working in **either TMSH or Bash contexts**, it’s essential to be mindful of the commands you issue. Incorrect or careless actions can negatively impact system operations, disrupt services, or even cause outages. Always double-check commands and ensure that they align with the intended task before executing them.

Understanding when and how to use these contexts correctly will give you greater control over the system while ensuring its stability and operational integrity.

Task 1. Listing URL Categories 
------------------------------

    In this task, you will use the TMSH CLI. This will help you understand the current categorization of URLs and how they are organized within the system.

    #. Access the BIG-IP SSLO-1 instance using the WebShell. A new browser tab will open with the BIG-IP Shell with Root logged in.

    #. Issue the CLI command to list one of the URL categories.

        CLI command::

            tmsh (Press ENTER to enter TMSH context from bash)
            list sys url-db url-category (Press TAB for auto-complete)

    #. When you press Tab at this point in the command, the auto-complete will ask you if you want **"Display all 221 items? (y/n)"**. Press **"y"** to see the full list of **Options, Properties and Configuration Items** 
    
        The list will be too long for the shell window, so pressing the **SPACE BAR** will page through to the end of the list. When you come to the **END** of the list, press **'q'** to exit the listing and return to the partial command.

    #. Scroll through the output and you'll see that the **Configuration Items** section is the list of URL categories that are currently configured on the system. This includes both built-in categories that come with the system and any custom categories that have been created.

        Notice our custom categories; **custom-allow-category** and **custom-block-category** are listed at the end of the listing. These are at the end because their names start with lower case letters. All built-in categories start with upper case letters and are listed at the beginning.

    #. Complete the command by typing **Sports**, which is one of the built-in URL categories. Remember the category names are case-sensitive.

        CLI command::

            list sys url-db url-category Sports

        The output will look similar to the below::

            sys url-db url-category Sports {
                cat-id 24617
                cat-number 18
                default-action allow
                description "Sites that provide information about or promote sports, active games, and recreation."
                display-name Sports
                f5-id 16525

        There are no URLs listed under this category since it is a built-in category that is maintained by F5 and updated through URL Category Database updates.

    #. Press the **UP ARROW** to recall the previous command and change the category name to list another built-in category; `Gambling` and review the output.

        **Optional** Try other built-in categories as well.

    #. Now issue the CLI command to list one of the custom URL categories.
    
        CLI command::

            list sys url-db url-category custom-allow-category

        The output will look similar to the below::

            sys url-db url-category custom-allow-category {
                cat-id 0
                cat-number 1904
                default-action allow
                display-name custom-allow-category
                f5-id 17004
                is-custom true
                urls {
                    https://\*chatgpt.com/ {
                        type glob-match
                    }
                    https://\*claude.com/ {
                        type glob-match
                    }
                    https://example.com/ { }
                }
            }

        Notice the various properties of the category including the **is-custom true** which indicates that this is a custom category. The URLs listed under the category include the two glob match patterns for any subdomains of chatgpt.com and claude.com, as well as an exact match for https://example.com/.

        Try listing the other custom category; `custom-block-category`.

    #. next

Task 2. Creating new Custom Categories
--------------------------------------

    #. Now you will create a new custom category using the TMSH CLI. This will allow you to understand how to define and manage custom categories within the system.

        TMSH command::

            create sys url-db url-category my-category display-name my-category default-action allow
            
        This command creates a new custom category named **my-category** with a default action of **allow**. This custom category also is empty; meaning no URLs are associated with it. You can verify that the category was created by listing it using the command from Task 1.

    #. Let's create a new custom category with URLs associated with it. 

        TMSH command::

            create sys url-db url-category my-category-1 display-name my-category-1 default-action allow urls add { https://www.example.com/ { type exact-match } } 

    #. List the category to verify that it was created with the URL.

        TMSH command::

            list sys url-db url-category my-category-1

        The output will look similar to the below::

            sys url-db url-category my-category-1 {
                cat-id 0
                cat-number 1905
                default-action allow
                display-name my-category-1
                f5-id 17005
                is-custom true
                urls {
                    https://www.example.com/ 
                }
            }

    #. Press the **UP ARROW** to recall the previous command add the option for **all-properties** to see the full details of the category including the URL properties.

        TMSH command::

            list sys url-db url-category my-category-1 all-properties

Task 3. Modifying Custom Categories
-----------------------------------

    #. Now you will modify an existing custom category using the TMSH CLI. This will help you understand how to update and manage custom categories as needed.

        CLI command::

            modify sys url-db url-category my-category urls add { https://www.newsite.com/ { type exact-match } }

        This command adds a new URL to the existing **my-category**. You can verify that the URL was added by listing the category again.

        **NOTE** The **{ type exact-match }** configuration option can be omitted as it is the default. The  must be specified when adding URLs that should match a pattern with a wildcard.


        **IMPORTANT** When adding URLs of the **type glob-match** using the **'*'** as a wildcard must be preceded by a backslash **'\'** to escape the wildcard character. This is required in the TMSH CLI to prevent the wildcard from being expanded by the shell before it is added to the category. For example, to add a glob match URL pattern for all subdomains of **newsite1.com**, you would use the following command::

             modify sys url-db url-category my-category urls add { https://\*.newsite1.com/ { type glob-match } }

Task 4. Deleting Custom Categories
-----------------------------------

    Using the TMSH CLI, you can also delete custom categories that are no longer needed.

    #. List the existing custom categories to identify the one you want to delete.
    
    #. Now you will delete an existing custom category using the TMSH CLI.

        CLI command::

            delete sys url-db url-category my-category

        This command deletes the custom category named **my-category**. You can verify that the category was deleted by trying to list it again, which should result in an error indicating that the category does not exist.

`Next Lab 7 - SWG Customizing Block Page <./lab_7_swg_customizing_block_page.rst>`__

`Main Page <./readme.md>`__