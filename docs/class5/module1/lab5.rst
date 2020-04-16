.. role:: raw-html(raw)
   :format: html

Update Service Chains on existing Security Policy rules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Update the existing Security Policy rules to use the new Service Chains you just created.

From the SSL Orchestrator **Configuration** screen:

-  Click the **Security Policies** tab in the middle of the main display area.

-  Click the Security Policy named **ssloP\_f5labs\_explicit**. This should be the only security policy in the list at this time.

-  Click on the pencil icon (|pencil|) next to the **Pinners\_Rule** to modify this rule.

-  In the properties section that appears, select **ssloSC\_Cisco\_TAP** from the **Service Chain** dropdown.

   |policy_rule_Cisco-TAP|

-  Click the **OK** button

-  Repeat the same process for the **Finance\_Bypass** rule

-  Now modify the **All Traffic** rule and select the **ssloSC\_all\_services** Service Chain and click the **OK** button.

-  The Security Policy Rules should now look like this:

   |updated_rules|

-  Click the **Deploy** button and then click the **OK** button on the pop-up to confirm you want to make the changes.

.. |pencil| image:: ../images/pencil.png
   :width: 20px
   :height: 20px
.. |policy_rule_Cisco-TAP| image:: ../images/policy_rule_Cisco-TAP.png
   :width: 466px
   :height: 89px
.. |updated_rules| image:: ../images/updated_rules.png
   :width: 1005px
   :height: 202px
