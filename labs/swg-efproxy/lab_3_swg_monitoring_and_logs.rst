Lab 3 - SWG Dashboard and Event Logs
=======================================

In this lab you will learn about the Dashboard and Event Logs for the Secure Web Gateway.  Monitoring and logging are essential for understanding how the SWG is performing, identifying potential issues, and ensuring that policies are being enforced correctly.

Task 1. Viewing SWG Dashboard
-----------------------------

    #. In to the BIG-IP TMUI, navigate to **Access > Overview > SWG Reports > Dashboard**

        .. image:: ./images/l3-access-swg-dashboard.png
            :align: center
            :alt: swg dashboard

        The SWG Dashboard provides an overview of the SWG activity, including metrics such as:
        
            - Top Host Names by Request Count
            - Top Security Categories by Blocked Request Count
            - Top Categories by Request Count
            - Top Categories by Blocked Request Count
            - Top Users by Request Count
            - Top Users by Blocked Request Count
  
        These metrics are provide by default, but you can also customize the dashboard to include other metrics that are relevant to your environment. The dashboard is a great place to get a quick overview of the SWG activity and identify any potential issues or trends in the traffic. 

        The 

Task 2. Viewing SWG Event Logs
------------------------

    #. In the BIG-IP TMUI, navigate to **Access > Overview > SWG Reports**
 
        .. image:: ./images/l3-access-event-logs.png
            :align: center
            :alt: event logs

        Here you can see a list of access events that have occurred on the system, including those related to the SWG. You can filter the logs by various criteria, such as date, user, or event type, to find specific entries related to SWG activity.    

    #. When making changes to URL Filters or Categories, remember to kill sessions so that the new policies are applied to the user traffic. As we did in Lab 2.

    #. Go to the Log configuration and select default log, and enable Allow Logs.

        .. image:: ./images/l3-access-logs-allow.png
             :align: center
             :alt: allow logs

    #. Close the browsers and kill the sessions again to generate logs for the allowed traffic.

    **TIP:** In production you will want to leave the Allow logs turned off,as it will generate many more logs, which will fill up the log storage more quickly. You can enable Allow logs temporarily when you need to generate logs for allowed traffic for troubleshooting or monitoring purposes.

More Information:

https://techdocs.f5.com/en-us/bigip-16-1-0/big-ip-access-policy-manager-secure-web-gateway/secure-web-gateway-statistics.html
https://techdocs.f5.com/en-us/bigip-16-1-0/big-ip-access-policy-manager-secure-web-gateway/logging-and-reporting.html


`Next Lab 4 - SWG Configuration <./lab_4_swg_configuration.rst>`__

`Main Page <./readme.md>`__