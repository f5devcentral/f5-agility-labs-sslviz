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

#. Below that, notice that the **REQUIRE_JUSTIFICATION** variable is set to ``0``.

   .. image:: ./images/user-justification-3.png
      :align: left

#. Change the ``0`` to ``1`` to enable this feature.

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

#. Navigate to https://chatgpt.com/. Now, the user coaching prompt appears but also includes a text box for users to enter a justification/reason for accessing that destination.

   .. image:: ./images/uc-user-justification-1.png
      :align: left

#. Enter ``research and testing`` in the text box and click on the **Submit** button to acknowledge the warning and terms of use policy. You will then be presented with the requested destination web site.


|

Review User Coaching Logs
--------------------------------------------------------------------------------

The user coaching iRule has logging enabled (currently local logging, but could be sent to an external log collector or SIEM). Let's take a look at what has been logged.

#. Return to the **BIG-IP SSL Orchestrator** **Web Shell** tab.

#. Enter ``grep ALERT-COACHING-TRIGGER /var/log/ltm`` to extract the user coaching logs from the LTM log file. You should see log entries similar to the following: ``ALERT-COACHING-TRIGGER::2026-01-25 13:44:42::client=10.1.10.50::host=chatgpt.com::justification=research+and+testing``

   .. image:: ./images/user-justification-7.png
      :align: left

