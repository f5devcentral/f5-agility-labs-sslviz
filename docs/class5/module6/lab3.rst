Accessing the BIG-IP CM API
================================================================================


Log into Central Manager UI
--------------------------------------------------------------------------------

The next step is to log into the BIG-IP Central Manager UI. In a purely
programmatic sense this is not expressly required, but we will use it in
this lab to provide visual cues to successful API deployment. You will
be able to see and interact with the applications created from the API.

#. From within the UDF interface, navigate to the **BIG-IP-Next-CM** instance and find the **GUI** access link.

#. Clicking this link opens a new browser tab to the CM logon screen.

#. Provide the credentials to log in.

#. On the home screen, click the **Manage Applications** button.

We will come back to the CM UI later. Let's now move on to using the CM API.


Login to Central Manager via API Request
--------------------------------------------------------------------------------

#. API requests to CM require an **Authorization: Bearer** token. To get that token you first need to make a login POST request to CM with your CM username and password.

   .. note::
      All of the following API calls will minimally include a **{{CM}}** variable value. This is a variable reference that points to a value in the included environments file. You can view these environment values in the Thunder client by navigating to the **Env** tab in the top left of the Thunder client navigation bar in Visual Studio Code, and then clicking on **sslo-environment**. Both user-defined variables, and variables captured from API responses are saved here.



   .. code-block:: text

      POST https://{{CM}}/api/login
      Content-Type: application/json

      {
         "username": "{{CM username}",
         "password": "{{CM password}"
      }


   This request returns a JSON payload with an **access_token** value that you will use for subsequent **Authorization: Bearer** token requests. The token will expire after a few minutes, so it may be necessary to regenerate this request periodically and fetch a new bearer token for subsequent API calls.


