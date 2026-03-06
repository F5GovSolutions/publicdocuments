Lab 4 - Manage Custom Categories using iControl Rest API
========================================================

Task 1. 
------------------------------

In this task, you will use the iControl REST API to list the custom categories that you have been working with in the previous labs. This will allow you to understand how to interact with the system programmatically and manage custom categories through the API.

        You can use a tool like Postman or curl to send REST API requests to the BIG-IP. The base URL for the API is `https://<BIG-IP-IP-ADDRESS>/mgmt/tm/`. You will need to authenticate using the credentials provided in the Details page of the BIG-IP instance.

        To list the custom categories, you can send a GET request to the following endpoint:

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
        "AU6PSXJL4MH2D5SWUNECBJZBTK"
        
        This command will return an authentication token that you can use in subsequent API requests to access the system. You can then use this token to send a GET request to the following endpoint to list the custom categories:
        