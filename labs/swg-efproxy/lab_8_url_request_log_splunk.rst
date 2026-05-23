Lab 8 - URL Request Logging with Splunk
=======================================

In this lab, you will configure URL request logging to send data to a Splunk instance.

Task 0. Run a Splunk Instance on Ubuntu Server
----------------------------------------------

    #. Using the WebShell of the Ubuntu Server and run the following command to start the Splunk instance.

        .. code-block:: bash

            docker run -d \
                -p 8000:8000 \
                -p 1514:1514 \
                --name splunk-test \
                -e "SPLUNK_GENERAL_TERMS=--accept-sgt-current-at-splunk-com" \
                -e "SPLUNK_START_ARGS=--accept-license" \
                -e "SPLUNK_PASSWORD=TestPassword123!" \
                splunk/splunk:latest

    #. Check the status of the Splunk instance by running the following command.

        .. code-block:: bash

            docker ps -a

    #. After logging in, you will be presented with the Splunk home page. You can use this interface to search and analyze the logs that are sent from the BIG-IP SSLO-1.


    #. Configure Data Inputs to add TCP port 1514 to receive logs from the BIG-IP SSLO-1. You can do this by navigating to Settings > Data Inputs > TCP and adding a new TCP input on port 1514.

    #. TCP add new, enter port #.

    #. Select Source Type: syslog, and click Next.

    #. Review the settings and click Submit to create the new TCP input.

Task 1. Configure System Logging Settings
-----------------------------------------

    #. Navigate to the BIG-IP SSLO-1 web interface and log in with your credentials.

    #. Create Pool and Pool member with Splunk Server IP Address and Port 1514.

    #. Create Logging Destination with the following settings:

        - Name: Splunk_Logging
        - Type: Remote High Speed Logging
        - Pool: <Splunk Pool created>
        - Protocol: TCP
        - Distribution: Adaptive

    #. Create another Logging Destination with the following settings:

        - Name: Splunk_Logging_formatted
        - Type: splunk
        - Forward to: Splunk_Logging (the Logging Destination created in the previous step)

    #. Create a Log Publisher

        - Name: Splunk_Logging_Publisher
        - Destination > Selected: Splunk_Logging_formatted (the Logging Destination created in the previous step)

Task 2. Access SWG URL Request Logging Settings
-----------------------------------------------

    #. Navigate to Access > Overview > Event Logs > Settings

    #. Create New APM Log Settings with the following settings:

        - Name: Splunk_SWG_URL_Request_Settings
        - Check the box for "Enable URL Request Logs"
    #. Click URL Request Logs in the left hand pane. Select the Log Publisher created in Task 1, 
      (Splunk_Logging_Publisher) from the drop-down menu.

    #. Check the boxes for Log Allowed Events, Log Blocked Events & Log Confirmed Events.

    #. Click Access Profile in the left hand pane. Select the Access Profile: F5 SWG M accessProfile that the SSLO created in Lab 4.1 from right hand pane and move it to the left hand pane using the arrow button.

Task 3. Verify SWG URL Request Logging
--------------------------------------

    #. Return to the Windows 11 client and open a web browser. Navigate to several websites that are allowed or blocked by the SWG policy.

    #. Return to the Splunk instance and configure it to automate field extractions for the URL request logs. You can do this by navigating to Settings > Fields > Field Extractions and creating a new field extraction for the URL request logs.

    #. Click New Field Extraction.Set the following fields in the form:
    
        - Name: URL_Request_Extraction
        - Destination app: search
        - Apply to: source type: syslog
        - Type: Inline
        - Extraction: Use the following regular expression to extract the relevant fields from the logs:

            .. code-block:: regex

                ^(?<timestamp>\S+)\s+(?<host>\S+)\s+(?<source>\S+)\s+(?<event_type>\S+)\s+(?<url>\S+)\s+(?<user>\S+)\s+(?<action>\S+)$

        Alternatively, you can use the following regular expression to extract key-value pairs from the logs:

            .. code-block:: key value pair

                (?<_KEY_1>[a-zA-Z0-9_\-]+)\s*=\s*"(?<_VAL_1>[^"]+)"

    #. Navigate to the Search & Reporting app. Use the search bar to search for logs related to the URL requests made from the Windows 11 client. You can use filters and keywords to narrow down the search results. For instance you can put this in the search bar to find all blocked URL requests:

        .. code-block:: search

            search action=blocked
        
        .. image:: ./images/l11-splunk-search.png
            :align: center
            :alt: Customizations