Scenario
--------

With the increase in the number of security incidents that have made the
news lately, your organization has updated its security policy to log
all user traffic flowing through the SSL Orchestrator irrespective of
whether the traffic has been inspected or bypassed. A new appropriately
sized Cisco Firepower TAP device has been purchased and has been cabled
to the SSL Orchestrator device. As the SSL Orchestrator Administrator,
your manager is asking you to do the following:

1) In addition to the intercepted traffic being inspected by the Squid
   Proxy service, the traffic needs to be copied to a new security service, a Cisco Firepower

2) Traffic that was previously bypassed and sent directly to the internet needs to be copied (still encrypted) to the Cisco Firepower

Lab Overview
------------

This lab assumes familiarity with SSL Orchestrator. The lab is
pre-staged with a deployment that is already configured with the
following Security Policy

.. image:: ../images/image005.png
   :align: center

You will modify the above Security Policy to satisfy the requirements from
the Scenario described.
