Class 1: SSL Orchestrator 2.0
=============================

F5 SSL Orchestrator (SSLO) provides an all-in-one appliance solution
designed specifically to optimize the SSL infrastructure, provide
security devices with visibility of SSL/TLS encrypted traffic, and
maximize efficient use of that existing security investment. This
solution supports policy-based management and steering of traffic flows
to existing security devices, designed to easily integrate into existing
architectures, and centralizes the SSL decrypt/encrypt function by
delivering the latest SSL encryption technologies across the entire
security infrastructure.

**Multi-Layered Security**

In order to solve specific security challenges, security administrators
are accustomed to manually chaining together multiple point products,
creating a bare-bones “security stack” consisting of multiple services.
A typical stack may include components like Data Leak Prevention (DLP)
scanners, Web Application Firewalls (WAF), Intrusion Prevention and
Detection Systems (IPS and IDS), Malware Analysis tools, and more. In
this model, all user sessions are provided the same level of security,
as this “daisy chain” of services is hard-wired.

**Dynamic Service Chaining**

Dynamic Service Chaining processes specific connections based on context
provided by the Classification Engine. These service chains can include
four types of services (Layer 2 in-line services, Layer 3 in-line
services, receive-only services, and ICAP services) you define, as well
as any decrypt zone between separate ingress and egress devices).

**Classification Engine**

Classification Engine provides a rich set of methods based on context to
dynamically determine how best to optimize the flow through the security
stack. Context can come from the following:

-  Source IP/subnet

-  Destination IP/subnet

-  IP intelligence category - Subscription

-  IP geolocation

-  Host and domain name

-  URL filtering category - Subscription

-  Destination port

-  Protocol

.. toctree::
   :maxdepth: 2
   :caption: Contents:
   :glob:

   labinfo
   module*/module*
   appendix*