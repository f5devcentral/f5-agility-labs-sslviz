Module 4 - Create an SSLO for Existing Applications
===================================================

SSL Orchestrator defines an existing application as a typical reverse proxy LTM
virtual server, performing its own SSL handling and traffic management. The
Existing Application SSLO topology therefore only needs to create the
components that this virtual server can consume, specifically the services,
service chains, and security policy. The Existing Application SSLO workflow
skips SSL management and interception rules, and ultimately produces an
SSLO-type per-request policy that can be attached to an existing LTM virtual
server.

.. note:: This lab will consist of an abbreviated set of steps, as all of the
   relevant objects created in Lab 1 (services, service chains and security
   policies) will be fully re-usable here. If any of these objects have not
   been created, please review Lab 1 for more detailed configuration
   instructions.

.. toctree::
   :maxdepth: 1
   :glob:

   lab*
