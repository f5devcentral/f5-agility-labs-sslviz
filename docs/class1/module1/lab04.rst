.. role:: red
.. role:: bred

Guided configuration topology
================================

.. image:: ../images/gc-path-1.png
   :align: center
   :scale: 50

SSLO creates discrete configurations based
on the selected topology. For example, in previous versions of SSLO,
a transparent and explicit forward proxy might be defined together.
In SSLO 5.0 and above, these are configured separately. An explicit
forward proxy topology will ultimately create an explicit proxy
listener and its relying transparent proxy listener, but the
transparent listener will be bound only to the explicit proxy tunnel.
If a subsequent transparent forward proxy topology is configured, it
will not overlap the existing explicit proxy objects. The Topology
Properties page provides the following options:

**For this lab:**

.. note:: The only fields that need to be edited are the ones explicitly mentioned in these bullets.  The other fields may be left with their default value.

-  **Name**: Enter some name (ex. ":red:`demoL3`").

.. TIP::

   As a general rule, avoid using names with dashes (ex. sslo-demo-1)
   while creating objects in SSL Orchestrator. Underscores (ex. sslo_demo_1)
   and camel-casing (ex. ssloDemo1) are preferred.

-  **Protocol**: Select :red:`Any` - this will create separate
   TCP, UDP and non-TCP/UDP interception rules.

-  **IP Family**: Select :red:`IPv4`

-  **Topology**: Select :red:`L3 Outbound`

   .. image:: ../images/module1-44.png
      :align: center
      :scale: 50


The **Topology** settings have been configured.

Click :red:`Save & Next` to continue to the next stage.

.. image:: ../images/module1-4.png
   :scale: 50 %
   :align: center

.. note:: There are no additional hands-on steps that need to be taken before proceeding to the next section.  The information below is intended to provide additional context on the Topology.


The **Protocol** option presents four protocol types:

-  **TCP** - this option creates a single TCP wildcard interception
   rule for the L3 Inbound, L3 Outbound, and L3 Explicit Proxy
   topologies.

-  **UDP** - this option creates a single UDP wildcard interception
   rule for L3 Inbound and L3 Outbound topologies.

-  **Other** - this option creates a single any protocol wildcard
   interception rule for L3 Inbound and L3 Outbound topologies,
   typically used for non-TCP/UDP traffic flows.

-  **Any** - this option creates the TCP, UDP and non-TCP/UDP
   interception rules for outbound traffic flows.

The SSL Orchestrator **Topologies** option page presents six
topologies:

-  **L3 Explicit Proxy** - this is the traditional explicit forward
   proxy.

-  **L3 Outbound** - this is the traditional transparent forward
   proxy. An L3 outbound topology is effectively a "routed hop"
   configuration, where the SSLO topology listener becomes a routed
   path on the way to external (ie. Internet) resources.

-  **L3 Inbound** - this is a reverse proxy configuration. Like the
   L3 outbound, L3 inbound is typically a routed hop configuration
   for traffic directed inbound. It can also behave as a traditional
   load-balanced application.

-  **L2 Inbound** - the layer 2 topology options insert SSLO as a
   bump-in-the-wire in an existing routed path, where SSLO presents
   no IP addresses on its outer edges. The L2 Inbound topology
   provides a transparent path for inbound traffic flows.

-  **L2 Outbound** - the layer 2 topology options insert SSLO as a
   bump-in-the-wire in an existing routed path, where SSLO presents
   no IP addresses on its outer edges. The L2 Outbound topology
   provides a transparent path for outbound traffic flows.

   .. note:: It is important to distinguish SSLO's layer 2 topology from those
      of other traditional layer 2 SSL visibility vendors. Layer 2
      solutions such as the Symantec SSL visibility appliance (SSLVA)
      limit the types of devices that can be inserted into the
      inspection zone to layer 2 and below, and devices must be directly
      connected to the appliance. An SSLO layer 2 topology only exists at
      the outer edges. Inside the inspection zone, full-proxy routing is
      still happening, so layer 3 and HTTP services can still function
      normally.

-  **Existing Application** - this topology is designed to work with
   existing LTM applications. Whereas the L3 Inbound topology
   provides an inbound gateway function for SSLO, Existing
   Application works with LTM virtual servers that already perform
   their own SSL handling and client-server traffic management. The
   Existing Application workflow proceeds directly to service
   creation and security policy definition, then exits with an
   SSLO-type access policy and per-request policy that can easily be
   consumed by an LTM virtual server.


