Lab 5 - Manage Custom Categories using iControl Rest API
========================================================

In this lab, you will use the iControl REST API to manage custom URL categories on the BIG-IP. This will allow you to interact with the system programmatically, which is useful for automation and integration with other systems.

You can use a tool like Postman or curl to send REST API requests to the BIG-IP. The base URL for the API is `https://<BIG-IP-IP-ADDRESS>/mgmt/tm/`. You will need to authenticate using the credentials provided in the Details page of the BIG-IP instance.

Task 0. Using Token Authentication
----------------------------------


        curl command::

            curl -sku 'admin:f5Twister!' -H 'Content-Type: application/json' -X GET 'https://10.1.1.6/mgmt/tm/sys/url-db/url-category/custom-block-category' | jq

        This command uses basic authentication with the username and password to send a GET request to the endpoint for the `custom-block-category` URL category. The response is then piped to `jq` for formatting.

    #. Retrieve an authentication token using the following command. Replace `username` and `password` with the appropriate credentials for your BIG-IP instance.
    
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

        This command will return an authentication token that you can use in subsequent API requests to access the system. You can then use this token to send a GET request to the following endpoint to list the custom categories:
        
    #. Next 



`Next Lab 6 - Manage Custom Categories using the CLI <./lab_6_swg_manage_cli.rst>`__

`Main Page <./readme.md>`__