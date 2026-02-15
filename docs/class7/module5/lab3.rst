Implement SaaS Tenant Isolation
==============================================================================

You will now enable and test the **tenant isolation** functionality. This will insert headers into the HTTP request to identify the tenants which would be allowed for the SaaS application. This can be setup for users to only use a specific tenant(s) to prevent users from copying data between tenants.

We are going to inspect the iRule to get an idea of the various services you can configure, and what we will use for testing the functionality in this lab. 

You will then test before configuring SSLO by going to https://httpbin.org/headers in your **Ubuntu-Client** WEBRDP session. This will show the missing tenant control headers. Then, after modifying the configuration, you will test against that site again to show how the headers are properly inserted.



Inspect iRule *saas-tenant-rule*
--------------------------------------------------------------------------------

#. Go to your **BIG-IP SSLO** GUI tab and navigate to **Local Traffic > iRules** and click on the **saas-tenant-irule** iRule to view the contents. There are 250 lines to the rule, and most of that is comments to help the user understand the functionality of the iRule.  

   .. note::

      **Do not change anything at this time. This is only to show the extent of the iRule**

      *For testing purposes, a separate "USE_TESTING" control has also been included, hardcoding a set of headers, and httpbin.org as the trigger URL.*

#. Please focus on lines 125-135 of the iRule. This is where we will test the proper insertion of headers for this lab. This section sets the static variable and array to define what headers and values are to be inserted.

   .. image:: images/saas-irule-lab-test.png
      :align: left

#. Now go to lines 241-248. This section executes the action based on the match of the URL. In this case, we are matching against httpbin.org. This is so we can actually see the headers being inserted.

   .. image:: images/saas-irule-action.png
      :align: left


#. Now hit the back button on the browser to get out of the iRule view, and lets test the functionality before adding new Service Extension.




View the reported headers before adding the SaaS Tenant Isolation Service
--------------------------------------------------------------------------------

#. Return to the **Ubuntu-Client** WEBRDP session.

#. Close the **Firefox** browser window and restart the application.

#. Navigate to the following URL: 

   .. code-block:: text

      https://httpbin.org/headers


#. You should **not** see the X-Test-Header-1 or X-Test-Header-2 headers in the response. You will see something similar the following:

   .. image:: images/saas-headers-missing.png
      :align: left



#. Lets get back to the SSL Orchestrator UI and update the Interception Rule and Service Chain to use this Service Extension. 

Click on the **SSL Orchestrator** tab on the left side of the GUI, and then click **Configuration**.


Add SaaS Tenant Isolation to the existing *combined_chain* Service Chain
--------------------------------------------------------------------------------

It's time to add the SaaS Isolation Service to the existing Service Chain that was created in the previous lab.

#. Click on the **Service Chains** tab and click the existing Service Chain **ssloSC_combined_chain**.

   .. image:: ./images/saas-service-chain.png
      :align: left

#. The name field is already filled out as we are amending the existing Service Chain.

#. Double-click on the **ssloS_F5_SaaS-Tenant-Isolation** Service to add to the Selected Service Chain Order.

   .. image:: ./images/saas-service-chain-add.png
      :align: left

#. Click **Deploy** and then **OK** to acknowledge the warning.  Click **OK** again after the deployment has completed.



Test SaaS Tenant Isolation
--------------------------------------------------------------------------------

#. Return to the **Ubuntu-Client** WEBRDP session.

#. Close the **Firefox** browser window and restart the application.

#. Navigate to the following URL: 

   .. code-block:: text

      https://httpbin.org/headers


#. Now you will see both the X-Test-Header-1 or X-Test-Header-2 headers in the response. 

   .. image:: images/saas-headers-inserted.png
      :align: left


This completes the installation, configuration and testing of the **SaaS Tenant Isolation Service Extension**.