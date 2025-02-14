Implement User Coaching
==============================================================================

You will now enable and test the **user coaching** functionality. This will produce a prompt in the web browser when a user attempts to connect to a *risky* web site.



Modify Interception Rule
--------------------------------------------------------------------------------

#. In the **SSL Orchestrator UI**, click on the **Interception Rules** tab.

   .. image:: ./images/user-coaching-1.png
      :align: left


#. Click on the **sslo_l3_outbound-in-t-4** Interception Rule to view the **Summary** page.

   .. image:: ./images/user-coaching-2.png
      :align: left


#. Click on the **Edit** (pencil) icon to view the settings.

#. Scroll down to the **Resources > iRules** section and double-click on the **/Common/user-coaching-ja4t-rule** iRule to add it to the **Selected** panel.


   .. image:: ./images/user-coaching-3.png
      :align: left


#. Click on the **Save & Next** button to return to the **Summary** page.

   .. image:: ./images/user-coaching-4.png
      :align: left


#. Click on the **Deploy** button.

#. When the deployment has completed, click on the **OK** button to close the dialog box and return to the **Topologies** list.


|

Add User Coaching Inspection Service to a Service Chain
--------------------------------------------------------------------------------

Create a new service chain that contains the user coaching service.


#. Click on the **Service Chains** tab.

   .. image:: ./images/user-coaching-5.png
      :align: left


#. From the **Service Chain List**, click on the **Add** button.

#. Enter ``user_coaching`` in the **Name** field.

#. Double-click on the **ssloS_F5_UC** and **ssloS_F5_FEYE** Inspection Services to add them to the Service Chain. The **ssloS_F5_AWAF** service will not be used for outbound inspection.

   .. image:: ./images/user-coaching-6.png
      :align: left


#. Click on the **Deploy** button.

#. When the deployment has completed, click on the **OK** button to close the dialog box and return to the **Topologies** list.

#. Click on the **Service Chains** tab to confirm that the new **Service Chain** was created.

   .. image:: ./images/user-coaching-7.png
      :align: left


Update the Security Policy
--------------------------------------------------------------------------------

The final step is to update the **Security Policy** to use the new **Service Chain**.

#. Click on the **Security Policies** tab to view the list of policies.

#. Click on the **ssloP_l3_outbound** policy to edit it.

   .. image:: ./images/user-coaching-8.png
      :align: left

#. Click on the **Edit** (pencil) icon for the **All Traffic** rule.


   .. image:: ./images/user-coaching-9.png
      :align: left


#. Set **SSL Proxy Action** to **Intercept**.

#. Set **Service Chain** to **ssloSC_user_coaching**.

   .. image:: ./images/user-coaching-10.png
      :align: left

#. Click on the **OK** button to exit edit mode.

   |

   Your **Security Policy** should now look like the following:

   .. image:: ./images/user-coaching-11.png
      :align: left


#. Click on the **Deploy** button and then click on **Deploy** again to accept the warning.

   .. image:: ./images/user-coaching-12.png
      :align: left

#. When the deployment has completed, click on the **OK** button to close the dialog box and return to the **Topologies** list.


|

Trigger Conditions for User Coaching
--------------------------------------------------------------------------------

The presentation of the user coaching prompt is determined by a URL category match. The category list is defined in the **user-coaching-rule** iRule.

#. Navigate to **Local Traffic > iRules** and verify that the following iRules are present.

#. Click on the **user-coaching-rule** iRule to view it.

#. Notice that the **COACHING_CATEGORIES** variable defines an array of URL categories.

   .. image:: images/user-coaching-trigger.png
      :align: left

   |

   .. note::

      Per the iRule comments, you can query the URL Category Database to determine the category names to use here. Do not change anything at this time.

|

Test User Coaching
--------------------------------------------------------------------------------

#. Return to the **Ubuntu-Client** WEBRDP session.

#. Close the **Firefox** browser window and restart the application.

#. Navigate to https://copilot.microsoft.com/. You should receive the SSL Orchestrator user coaching prompt as follows:

   .. image:: ./images/user-coaching-13.png
      :align: left


#. Click on the **Agree** button to acknowledge the warning and terms of use policy. You will then be presented with the Microsoft Copilot site.

   .. image:: ./images/user-coaching-14.png
      :align: left

#. Restart **Firefox** and browse to Copilot again. You should not see the prompt reappear because the original user coaching acknowledgement has not expired yet.

   .. note::

      The default user coaching session timeout setting is 3600 seconds. This value is configurable in the **user-coaching-rule** iRule.

