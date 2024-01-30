Accessing the BIG-IP Central Manager API
================================================================================

Log into Central Manager via API Request
--------------------------------------------------------------------------------

API requests to BIG-IP CM require an access token, which you can obtain by sending an HTTP POST request to the BIG-IP CM's **login** API endpoint. You must authenticate with your username and password.

Here is the what that API call looks like:

.. code-block:: text

   POST https://{{CM}}/api/login
   Content-Type: application/json

   {
      "username": "{{CM username}",
      "password": "{{CM password}"
   }

A similar API request has already been created for you and is stored in the SSL Orchestrator Collection.

#. In the **Create SSLO Deployment** folder, click on the **CM Login** request to select it.

   .. image:: ./images/login-1.png


#. Click on the **Send** button to submit the request to the BIG-IP CM API. 


   This request returns a JSON payload with an **access_token** value that you will be used for subsequent **Authorization: Bearer** token requests. 

   .. image:: ./images/login-2.png


#. Click on the **Tests** tab and then click on the **Scripting** tab.

   .. image:: ./images/login-3.png

   This script extracts the **access_token** attribute value and stores it in the **authToken** variable. Recall that the **authToken** value was present in the Environment variables list.


   .. important::
      The token will expire after a few minutes, so it will be necessary to resend this request periodically to fetch a new access token for subsequent API calls.

      You will receive an HTTP **401 Unauthorized** status and a message stating that your **access token expired**.

      .. image:: ./images/login-expired.png


#. In the **Create SSLO Deployment** folder, click on the **Get BIG-IP Instances** request to select it.

#. Click on the **Headers** tab (below the request URL).

   .. image:: ./images/login-4.png

   Notice that the **Authorization** header contains a value of **Bearer {{authToken}}**. API calls containing valid access tokens are accepted by the BIG-IP CM API without having to provide login credentials again. The **Authorization** header contains the **access_token** that was returned when you previously logged in using the **CM Login** API call.

