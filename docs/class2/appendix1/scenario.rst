Scenario
==========

Your organization is experiencing outbound Office 365 application latency issues. You have determined that this traffic is being decrypted and sent through your web gateways (HTTP proxies). Microsoft recommends bypassing outbound web gateways and SSL interception due to an impact on Office 365 application performance.

`Microsoft Reference <https://docs.microsoft.com/en-us/microsoft-365/enterprise/managing-office-365-endpoints?view=o365-worldwide>`_


Lab Overview
=============

With the understanding that there is not much value in applying URL filtering and content caching to Office 365 traffic, you are tasked with creating an SSL Orchestrator **Security Policy** rule that bypasses both SSL decryption and your web gateway service.

.. note::
   This lab depends on having a working SSL Orchestrator outbound topology.
