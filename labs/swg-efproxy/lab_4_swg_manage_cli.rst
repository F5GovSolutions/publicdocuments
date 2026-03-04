Lab 4 - Manage Custom Categories and Filters using the CLI
==========================================================

Task 0. TMSH and bash Contexts

**Understanding TMSH and Bash CLI Contexts**

In this lab, you will be working directly with the BIG-IP system using both **TMSH** (Traffic Management Shell) and **Bash CLI** contexts. These interfaces provide powerful ways to interact with the system, each serving distinct purposes and offering specific functionality.

- **TMSH (Traffic Management Shell)**: 
  - TMSH is the primary administrative interface for managing and configuring BIG-IP systems. It provides a structured and intuitive way to interact with system objects, configuration settings, and operational data.
  - Using TMSH allows you to make changes to BIG-IP configurations, retrieve statistical data, and interact with the system in a controlled manner. It is directly tied to the BIG-IP management framework and ensures safety and consistent behavior within the system.

- **Bash CLI**:
  - Bash CLI provides direct access to the underlying operating system of the BIG-IP system. It is more low-level and powerful, enabling you to manage files, troubleshoot issues, and run advanced administrative commands.
  - While Bash CLI offers flexibility, it also requires caution as improper commands can impact the system’s functionality or stability.

**Important: Be Careful with Commands**

When working in **either TMSH or Bash contexts**, it’s essential to be mindful of the commands you issue. Incorrect or careless actions can negatively impact system operations, disrupt services, or even cause outages. Always double-check commands and ensure that they align with the intended task before executing them.

Understanding when and how to use these contexts correctly will give you greater control over the system while ensuring its stability and operational integrity.

Task 1. Listing URL Categories 
------------------------------

    In this task, you will use the TMSH CLI. This will help you understand the current categorization of URLs and how they are organized within the system.

    #. Access the BIG-IP SSLO-1 instance using the WebShell. A new Shell tab will open.

    #. Issue the CLI command to list the URL categories::

        list sys url-db url-category custom-allow-category

        You should see the output::

            sys url-db url-category custom-block-category {
                cat-id 0
                cat-number 1905
                description htt
                display-name custom-block-category
                f5-id 17005
                is-custom true
                urls {
                    https://blockme.com\* {
                        type glob-match
                    }
                }
            }


    #. 




Task 2. Creating new Custom Categories
--------------------------------------



Changing Custom Categories.


`Next Lab 5 - SWG Explict Forward Proxy Configuration <./lab_3_swg_configuration.rst>`__

`Main Page <./readme.md>`__