.. role:: red
.. role:: bred

Scenario
================================================================================

Your manager lets you know that the company's updated security policy requires the logging of usernames for all intercepted traffic. You are tasked with developing a working Proof of Concept and are asked to come up with an action plan to do so, with the following restrictions:

-  This process needs to be transparent to a user that has already authenticated to the domain (ex. is logged into a domain-joined computer)


Lab Overview
================================================================================

In this lab, you will configure SSL Orchestrator to enable NTLM authentication and provide the authenticated username to the Squid security service where it can be logged with each HTTP request.

.. note::
   The Access Policy and associated authentication objects required for this lab have already been configured for you.

