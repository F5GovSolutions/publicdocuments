Lab 5 - Manage Custom Categories using iControl Rest API
========================================================

In this lab, you will become familiar with the iControl REST API to manage custom URL categories on the BIG-IP. This will allow you to interact with the system programmatically, which is useful for automation and integration with other systems.

References:
    https://clouddocs.f5.com/api/icontrol-rest/
    https://my.f5.com/manage/s/article/K51731137

You can use a tool like Postman or curl to send REST API requests to the BIG-IP. You will need to authenticate using the credentials provided in the Details page of the BIG-IP instance.


Task 0. Using Token Authentication
----------------------------------

        curl command::



        This command uses basic authentication with the username and password to send a GET request to the endpoint for the `custom-block-category` URL category. 
        
        **NOTE:** The response is then piped to `jq` for formatting.

    #. Retrieve an authentication token using the following command. Replace `username` and `password` with the appropriate credentials for your BIG-IP instance.
    
        This command will return an authentication token that you can use in subsequent API requests. Copy the token value from the output, as you will need it for the next steps.

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
        "<SOME-STRING-OF-CHARACTERS>"

    #. Next 

Task 1. iControl REST API
-------------------------

    Using the iControl REST API, you can perform various operations to manage custom URL categories on the BIG-IP. Below are examples of how to list, create, modify, and delete custom categories using curl commands.

    #. Listing Categories using the API

        curl command::

            curl -sk https://<BIG-IP-IP-ADDRESS>/mgmt/tm/sys/url-db/url-category/custom-block-category | jq

            curl -sku 'admin:f5Twister!' -H 'Content-Type: application/json' -X GET 'https://10.1.1.6/mgmt/tm/sys/url-db/url-category/custom-block-category' | jq

    #. Creating Custom Categories using the API

        curl command::

            curl -sk https://

    #. Modifying Custom Categories using the API

        curl command::

            curl -sk https://

    #. Deleting Custom Categories using the API

        curl command::

            curl -sk https://  


Task 2. [Optional] urlupdater Script
------------------------------------

    The urlupdater script is a Bash script that can be used to automate the management of URL categories on the BIG-IP. It uses the iControl REST API to perform operations such as adding or removing URLs from categories, creating new categories, and more.

    You can find the script in the F5 DevCentral GitHub repository:
    https://github.com/kevingstewart/sslo-custom-url-category-update-rest/tree/2.1

    use this script to simplify repetitive tasks and ensure consistency in your URL category management.



`Next Lab 6 - Manage Custom Categories using the CLI <./lab_6_swg_manage_cli.rst>`__

`Main Page <./readme.md>`__