.. role:: red
.. role:: bred

**Consolidation of Security with F5 SSL Orchestrator Secure Web Gateway as a Service (SWGaaS)** 
================================

Overview
--------

F5 SSL Orchestrator (SSLO) provides an all-in-one appliance solution
designed specifically to optimize the SSL infrastructure, provide
security devices with visibility of SSL/TLS encrypted traffic, and
maximize efficient use of that existing security investment. This
solution supports policy-based management and steering of traffic flows
to existing security devices, designed to easily integrate into existing
architectures, and centralizes the SSL decrypt/encrypt function by
delivering the latest SSL encryption technologies across the entire
security infrastructure.

**Multi-layered security**

In order to solve specific security challenges, security administrators
are accustomed to manually chaining together multiple point products,
creating a bare-bones "security stack" consisting of multiple services.
A typical stack may include components like Data Leak Prevention (DLP)
scanners, Web Application Firewalls (WAF), Intrusion Prevention and
Detection Systems (IPS and IDS), Malware Analysis tools, and more. In
this model, all user sessions are provided the same level of security,
as this "daisy chain" of services is hard-wired.

**Dynamic service chaining**

Dynamic service chaining effectively breaks the daisy chain paradigm by
processing specific connections based on context provided by the
Security Policy, that then allows specific types of traffic to flow
through arbitrary chains of services. These service chains can include
five types of services: layer 2 inline services, layer 3 inline
services, receive-only services, ICAP services, and HTTP web proxy
services.

**Topologies**

Different environments call for different network implementations. While
some can easily support SSL visibility at layer 3 (routed), others may
require these devices to be inserted at layer 2. SSL Orchestrator can
support all of these networking requirements with the following topology
options:


.. hlist::
   :columns: 2

   - Outbound transparent proxy
   - Outbound explicit proxy
   - Outbound layer 2
   - Inbound reverse proxy
   - Existing application
   - Inbound layer 2

**Security Policy**
   The SSLO Security Policy provides a rich set of context-aware methods to
   dynamically determine how best to optimize traffic flow through the security
   stack. Context can minimally come from the following:

.. hlist::
   :columns: 2

   - Source and destination address/subnet
   - URL filtering and IP intelligence (Subscriptions)
   - Host and domain name
   - Destination port
   - IP geolocation
   - Protocol

.. image:: images/introduction-1.png
