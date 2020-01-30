Scenario:
---------

With the increase in the number of security incidents that have made the
   news lately, your organization has updated its security policy to log
   all user traffic flowing through the SSL Orchestrator irrespective of
   whether the traffic has been inspected or bypassed. A new appropriately
   sized Cisco Firepower L2 device has been purchased and has been cabled
   to the SSL Orchestrator device. As the SSL Orchestrator Administrator,
   your manager is needing you to do the following things:

      1) In addition to the intercepted traffic being inspected by the Squid
      Proxy device, the traffic needs to be directed to the Cisco Firepower
      device

      2) For traffic that was being bypassed, the still encrypted traffic
      needs to be directed to the Cisco Firepower device

Lab overview:
-------------

This lab assumes familiarity with SSL Orchestrator. The lab is
   pre-staged with a deployment that is already configured with the
   following Security Policy

|image4|

Please modify the above Security Policy to satisfy the requirements from
   the Scenario described. Please following the step by step directions
   that follow to successfully complete this task.

.. |image4| image:: ../media/image005.png
   :width: 7.05556in
   :height: 1.40417in