Update Service Chains on existing Security Policy rules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Update the existing Security Policy rules to use the new Service Chains you just created.

From the SSL Orchestrator Configuration screen:

-  Click the **Security Policies** tab in the middle of the main display area.

-  Click the Security Policy named **ssloP\_f5labs\_explicit**.

-  Click on the pencil icon (|pencil|) next to the **Pinners\_Rule** to modify this rule.

-  In the properties section that appears, select **ssloSC\_CiscoFP\_TAP** from the **Service Chain** dropdown.

   |policy-rule-CiscoFP-TAP|


-  Click the **OK** button

-  Repeat the same process for the **Finance\_Bypass** rule

-  Now modify the **All Traffic** rule and select the **ssloSC\_All\_Services** Service Chain and click the **OK** button.

-  The Security Policy rules should now look like this:

   |updated-security-policy|


-  Click the **Deploy** button and then click the **OK** button on the pop-up to confirm you want to make the changes.



.. |pencil| image:: ../images/pencil.png
   :width: 20px
   :height: 20px
   :alt: pencil

.. |policy-rule-CiscoFP-TAP| image:: ../images/policy-rule-CiscoFP-TAP.png
   :alt: Policy rule for Cisco Firepower TAP service 

.. |updated-security-policy| image:: ../images/updated-security-policy.png
   :alt: Updated security policy
