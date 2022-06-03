.. role:: red
.. role:: bred

Transparent Authentication Using NTLM
================================================================================

While SSL Orchestrator is providing visibility into SSL traffic, a large amount of data may be collected and logged by the orchestrated security services. The volume of data and lack of easily identifiable client traffic can hinder troubleshooting efforts, especially if there are shared computers in the workplace or if users are coming from behind a NAT. In addition to facilitating more detailed logging, security services may use this additional information to make policy decisions (ex. an HTTP proxy allowing access to specific resources based on username or group membership).

SSL Orchestrator, combined with BIG-IP Access Policy Manager (APM), provides the ability to enable transparent passwordless authentication via NTLM and Kerberos. Data from the authenticated user (ex. username) can then be passed on to security services, such as an HTTP proxy service.

This lab takes you through the process required to enable NTLM authentication and to send the authenticated username to the Squid proxy service.

.. toctree::
   :maxdepth: 1
   :glob:

   scenario*
   lab*