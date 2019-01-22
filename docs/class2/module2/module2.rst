Module 2 - Create a Gateway Reverse Proxy SSLO
==============================================

SSL Orchestrator generally defines inbound traffic flows with a "gateway"
architecture. That is, SSLO is designed to sit in front of a separate ADC/load
balancer or routed path, and not directly in front of applications, though it
is technically possible to support a "single instance" listener going to a
single pool of resources. This lab will be re-using the security services
created in the first lab to create a single inbound "gateway" service SSLO
configuration.

.. note:: This lab will consist of an abbreviated set of steps, as some of the
   objects created in Lab 1 (services and service chains) will be fully
   re-usable here. If any of these objects have not been created, please review
   Lab 1 for more detailed configuration instructions.

.. toctree::
   :maxdepth: 1
   :glob:

   lab*
