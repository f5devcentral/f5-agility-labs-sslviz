Accessing the BIG-IP Central Manager API
================================================================================


Log into Central Manager (CM) GUI
--------------------------------------------------------------------------------

In a purely programmatic sense, it not required to log into the BIG-IP Central
Manager UI. However, you will use it in in this lab to provide visual feedback
on successful API deployment. You will be able to see and interact with the
application created from the API.

.. note::
   Skip this section if you are still logged into the BIG-IP CM GUI from the previous lab module.

#. Refer to section 3.1 of this Lab Guide to access and log into the BIG-IP CM GUI.

#. On the home screen, click the **Manage Applications** button.

You will come back to the BIG-IP CM GUI later. Let's now move on to using the BIG-IP CM API.


Log into Central Manager via API Request
--------------------------------------------------------------------------------

API requests to BIG-IP CM require an **Authorization: Bearer** token. To get that token you first need to make a login POST request to BIG-IP CM with your username and password.

Here is the what that API request looks like:

.. code-block:: text

   POST https://{{CM}}/api/login
   Content-Type: application/json

   {
      "username": "{{CM username}",
      "password": "{{CM password}"
   }

A similar API request has already been created for you and is stored in the SSL Orchestrator Collection.

#. In the **Collections** > **Create SSLO Deployment** folder, click on the **CM Login** request to select it.

   .. image:: ./images/login-1.png


#. Click on the **Send** button to submit the request to the BIG-IP CM API. 


   This request returns a JSON payload with an **access_token** value that you will use for subsequent **Authorization: Bearer** token requests. 

   .. image:: ./images/login-2.png

   .. note::
      The token will expire after a few minutes, so it may be necessary to regenerate this request periodically and fetch a new bearer token for subsequent API calls.

