Enable User Justification
==============================================================================

Let's take the **user coaching** functionality a step further by enabling the **user justification** option which requires the user to provide a reason for accessing that destination.


Modify User Coaching iRule
--------------------------------------------------------------------------------

#. In the **BIG-IP TMUI**, navigate to **Local Traffic > iRules**.

#. Click on the **user-coaching-rule** iRule to edit it.

   .. image:: ./images/user-justification-1.png
      :align: left

#. Notice that the coaching message text is defined as a variable called **COACHING_MESSAGE**. This allows you to customize the message based on your organization's policies. Do not change it at this time.

   .. image:: ./images/user-justification-2.png
      :align: left

#. Below that, notice that the **JUSTIFICATION_LOGGING** variable is set to **""** (empty string).

   .. image:: ./images/user-justification-3.png
      :align: left

#. In between the double quotation marks, enter ``on`` to enable this feature.

   .. image:: ./images/user-justification-4.png
      :align: left

#. Click on the **Update** button to save your change.

   .. image:: ./images/user-justification-5.png
      :align: left

|

Test User Justification
--------------------------------------------------------------------------------

#. Return to the **Ubuntu-Client** WEBRDP session.

#. Close the **Firefox** browser window and restart the application.

#. Navigate to https://copilot.microsoft.com/ again. Since you acknowledged the user coaching prompt previously (without requiring justification), you will not be prompted again.

#. Navigate to a new site: https://gemini.google.com/. Now, the user coaching prompt appears but also includes a text box for users to enter a justification/reason for accessing that destination.

   .. image:: ./images/user-justification-6.png
      :align: left

#. Enter ``research and testing`` in the text box and click on the **Submit** button to acknowledge the warning and terms of use policy. You will then be presented with the requested destination web site.


|

Review User Coaching Logs
--------------------------------------------------------------------------------

The user coaching iRule has logging enabled (currently local logging, but could be sent to an external log collector or SIEM). Let's take a look at what has been logged.

#. Return to the **BIG-IP SSL Orchestrator** **Web Shell** tab.

#. Enter ``grep ALERT-COACHING-TRIGGER /var/log/ltm`` to extract the user coaching logs from the LTM log file. You should see log entries similar to the following:

   .. image:: ./images/user-justification-7.png
      :align: left

