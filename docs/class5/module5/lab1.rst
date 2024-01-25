About Inbound Gateway Mode
==============================================================================

The SSL Orchestrator **inbound gateway mode** deployment describes a
scenario where the F5 BIG-IP functions in routing mode. The
destination addresses are behind the BIG-IP and traffic is forwarded through
as a routed next hop. This is different from the standard
application deployment because of the following attributes:

-  The virtual server listens on a wildcard (0.0.0.0/0) IP subnet, and
   optionally a wildcard (any) port.

-  No pool is assigned to the virtual server.

-  No destination address translation (NAT) is performed, however source address
   translation (SNAT) can still be used.

Aside from this, the SSL Orchestrator policy and inspection services are
attached in exactly the same way as other inbound application workflows.

.. image:: ./images/inbound-gw-mode.png


.. note::
   The following instructions assume basic connectivity to the lab
   environment, and administrative access to the lab's network and virtual
   machine configurations.

