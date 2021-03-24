.. role:: red
.. role:: bred

Scenario
================================================================================

With the increase in the number of security incidents that have made the news lately, your organization has updated its security policy to log all user traffic flowing through SSL Orchestrator, irrespective of whether the traffic will be inspected or bypassed. A new Cisco Firepower Threat Detection solution has been purchased and has been connected to the SSL Orchestrator device. As the Administrator of SSL Orchestrator, your manager is asking you to do the following:

1) In addition to sending Internet-bound traffic to a Squid proxy, this traffic needs to be inspected by the Cisco Firepower device

2) Traffic that was previously bypassed and sent directly to the Internet (skipping the Squid proxy) needs to be inspected by the Cisco Firepower device


Lab Overview
================================================================================

This lab assumes familiarity with SSL Orchestrator. This lab is pre-configured with the following Security Policy:

.. image:: ../images/initial-security-policy.png
   :alt: Initial Security Policy

By the end of this module you will have modified the existing Security Policy to satisfy the requirements from the scenario described.
