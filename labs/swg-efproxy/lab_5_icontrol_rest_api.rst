Lab 5 - Manage Custom Categories using iControl Rest API
========================================================

In this lab, you will become familiar with the iControl REST API to manage custom URL categories on the BIG-IP. This will allow you to interact with the system programmatically, which is useful for automation and integration with other systems.

You can use a tool like Postman or curl to send REST API requests to the BIG-IP. You will need to authenticate using the credentials provided in the Details page of the BIG-IP instance.

**NOTE:** Although possible, managing URL Filters through the iControl REST API is not recommended due to the complexity of the configuration and the potential for errors that could impact system behavior. It is recommended to manage URL Filters through the TMUI. Since the APM Policy only contains a single URL Filter with multiple URL categories, managing allowed and blocked URLs are primarily done by adding and removing URLs in those categories. Therefore, in this lab we will focus on managing URL Categories through the iControl REST API.

Task 0. Using Token Authentication
----------------------------------

    Before you can send API requests, you need to authenticate and obtain an authentication token. 
    
    #. Retrieve the authentication token using the following command. Replace `username` and `password` with the appropriate credentials for your BIG-IP instance.
    
        This command will return an authentication token that you can use in subsequent API requests.

        curl commands:: 
            curl -sk https://10.1.1.6/mgmt/shared/authn/login \
            -X POST \
            -H "Content-Type: application/json" \
            -d '{
               "username": "username",
               "password": "password",
               "loginProviderName": "tmos"
            }' | jq .token.token
     
        OUTPUT::
        "<AUTH-TOKEN-VALUE-OUTPUT>"

    #. Copy this token value off to a text editor and use it in the Authorization header for subsequent API requests.

Task 1. iControl REST API
-------------------------

    Using the iControl REST API, you can perform various operations to manage custom URL categories on the BIG-IP. Below are examples of how to list, create, modify, and delete custom categories using curl commands.

    #. Listing URL Categories using the API;

        curl command::

            curl -sk -H "X-F5-Auth-Token: <AUTH-TOKEN-VALUE-HERE>" \
                -H 'Content-Type: application/json' \
                -X GET "https://10.1.1.6/mgmt/tm/sys/url-db/url-category/custom-block-category" | jq

        This command retrieves the details of the `custom-block-category` URL category. The response will include information about the category, such as its name, display name, default action, and associated URLs.

        You can also list all URL categories by sending a GET request to the endpoint without specifying a category name. The path would be:

            https://10.1.1.6/mgmt/tm/sys/url-db/url-category

        This will return a full list of the URL categories configured on the BIG-IP, including both custom and default categories.

    #. Creating Custom Categories using the API

        curl command::

            curl -sk -H "X-F5-Auth-Token: <AUTH-TOKEN-VALUE-HERE>" \
            -H "Content-Type: application/json" \
            -X POST "https://10.1.1.6/mgmt/tm/sys/url-db/url-category" \
            -d '{
                "name": "my-custom-block-list",
                "displayName": "Custom Block List",
                "urls": [
                    { "name": "https://www.example-malware.com" }, 
                    { "name":"https://*.anothersite.com/", "type":"glob-match"
                    }
                        ],
                "description": "API created category"
                }' | jq

    #. Verify that the category was created by listing it using the GET command. Also you can go to the TMUI and navigate URL Categories.

    #. Modifying Custom Categories using the API

        curl command::

            curl -sk -H "X-F5-Auth-Token: <AUTH-TOKEN-VALUE-HERE>" \
            -H "Content-Type: application/json" \
            -X PATCH "https://10.1.1.6/mgmt/tm/sys/url-db/url-category/my-custom-block-list" \
            -d '{
            "urls": [
                { "name": "https://www.specific-site.com" },
                { "name": "https://*.glob-match-example.net/", "type":"glob-match" }
                    ]
            }' | jq

        **WARNING:** This command will replace the existing list of URLs in the `my-custom-block-list` category with the new list provided in the data. Be sure to include all URLs you want to be associated with the category in this command, as it will overwrite the previous list.

    #. Verify that the category was modified by listing it using the GET command. Also you can go to the TMUI and navigate URL Categories.

    #. Deleting Custom Categories using the API

        curl command::

            curl -sk -H "X-F5-Auth-Token: <AUTH-TOKEN-VALUE-HERE>" \
            -X DELETE \
            -H "Content-Type: application/json" \
            "https://10.1.1.6/mgmt/tm/sys/url-db/url-category/my-custom-block-list"

        **NOTE:** This command does not return a response body.
    
    #. Verify that the category was deleted by listing it using the GET command. Also you can go to the TMUI and navigate URL Categories.

References:
+++++++++++
    https://clouddocs.f5.com/api/icontrol-rest/
    https://my.f5.com/manage/s/article/K51731137


Task 2. [Optional] urlupdater Script
------------------------------------

    The urlupdater script is a Bash script that can be used to automate the management of URL categories on the BIG-IP. It uses the iControl REST API to perform operations such as adding or removing URLs from categories, creating new categories, and more.

    You can find the script in the F5 DevCentral GitHub repository:
    https://github.com/kevingstewart/sslo-custom-url-category-update-rest/tree/2.1

    **CAVEAT:** This script is an open source project with no official support from F5. It is provided as an example and may require modifications to work in your specific environment. Be sure to review the script and understand its functionality before using it.

    #. Access the Ubuntu Server's Web Shell.

    #. Go to the /urlupdater directory. List the contents of the directory to verify that the urlupdater script is present.  There are also some sample text files that can be used for testing.

        bash command::

            cd /urlupdater
            ll

    #. Run the script with the -h flag to see the available options and usage instructions.

        bash command::

            ./urlupdater.sh -h
    
    The script output provides the explanation for how to use it for managing URL categories, such as adding or removing URLs, creating new categories, and more. You can use these options to perform the desired operations on your BIG-IP instance.

`Next Lab 6 - Manage Custom Categories using the CLI <./lab_6_swg_manage_cli.rst>`__

`Main Page <./readme.md>`__