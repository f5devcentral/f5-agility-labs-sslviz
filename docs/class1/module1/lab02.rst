.. role:: red
.. role:: bred

Review the default SSL Orchestrator pre-requisites
===================================================

When
using the UDF blueprint, most of these have been pre-configured for you.
The only exception is the default route, which will be explicitly addressed
in a later section.

.. note:: There are no additional hands-on steps that need to be taken by the student before proceeding to the next section.  The information below is intended to provide additional context on the pre-requisites for a production environment.

-  **Import the CA certificate and private key** - in order to terminate and
   re-encrypt outbound SSL traffic, SSL Forward Proxy must re-issue, or rather
   "forge" a new server certificate to the client. In order to perform this
   re-issuance process, the BIG-IP must possess a certificate authority (CA)
   certificate and associated private key.
   :red:`This lab environment already has a subordinate CA certificate and
   private key installed.`

-  **Create the client inbound VLAN and self-IP** - create the VLAN and self-IP
   that connects the client to the BIG-IP. In this lab that's the
   :red:`10.1.10.0/24` subnet and interface :red:`1.1` on the BIG-IP.
   :red:`This lab environment already has this VLAN and self-IP created.`

-  **Create the Internet outbound VLAN and self-IP** - create the VLAN and
   self-IP that connects the BIG-IP to the outbound Internet router. In this lab
   that's the :red:`10.1.20.0/24` subnet and interface :red:`1.2` on the BIG-IP.
   :red:`This lab environment already has this VLAN and self-IP created.`

-  **Create the DLP/ICAP VLAN and self-IP** - if it is desired to isolate the
   DLP/ICAP device, create the VLAN and self-IP that connects the DLP device to
   the BIG-IP. In this lab that's the :red:`197.19.97.0/25` subnet and interface
   :red:`1.3 (tag 50)` on the BIG-IP. The DLP security device is listening on
   :red:`198.19.97.7` and ICAP is listening on port :red:`1344`.
   :red:`This lab environment already has this VLAN and self-IP created`.

-  **Create the default internet route for outbound traffic** - the iApp
   provides an option to leverage a defined gateway pool or use the system
   default route. If a gateway pool is not used, the system route table will
   need to have a default route used to reach Internet destinations.
   :red:`We will use a gateway pool defined within SSLO`.


.. TIP::

   As a general rule, avoid using names with dashes (ex. sslo-demo-1)
   while creating objects in SSL Orchestrator. Underscores (ex. sslo_demo_1)
   and camel-casing (ex. ssloDemo1) are preferred.
