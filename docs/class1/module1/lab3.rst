Lab 3: Create custom Service Chains
====================================

F5 has been a market leader in SSL/TLS technologies for many years, so
it should come as no real surprise to hear that the most powerful
attribute of the SSL Orchestrator is not actually SSL, but rather the
advanced networking “orchestration” capabilities of the BIG-IP full
proxy architecture. All of the competitors in the SSL visibility space
can re-issue (i.e. “forge”) server certificates, and most these days can
handle Perfect Forward Secrecy. But very few have the fundamental
qualities necessary to pull off intelligent service chaining. Let’s then
define what service chaining really means. Essentially, it is the
ability to intelligently assign, and re-use security services across
multiple decrypted/inspect-able traffic flows based on the
characteristics of those flows. Service chaining includes the ability
to:

-  Load balance security services

-  Monitor those security services and potentially skip them if they
   fail

-  Independently port translate across those security services

-  Assign and re-use a service in multiple "chains"

-  Steer "inspect-able" traffic through different chains based on
   attributes of a discreet packet

The implementation of service chaining manifests as three core functions
of the SSL Orchestrator product:

-  **Defining security services** – this is an exercise you’ve already
   completed if you went through Lab 1. It is the declaration of the
   service devices, inputs and outputs, and additional options specific
   to that service.

-  **Creating meaningful chains of security services** – a chain is a
   list of defined services through which inspect-able traffic should
   flow. You might, for example, have a chain dedicated to all HTTP
   traffic that could include passive, ICAP, L2 and L3 inline services,
   or traffic originating from or going to some address space that
   includes passive and L3 inline services, or traffic that meets some
   other business need that just includes a passive security service.
   You’ll create these chains as named objects that will be referenced
   from traffic classifiers.

-  **Intelligently selecting a chain based on various attributes of the
   data** – a traffic classifier is a logic engine that takes as input
   various attributes including source and destination addresses,
   destination port(s), host names, URL and IP intelligence categories,
   geographical information, and even some protocol awareness. You can
   create multiple discreet traffic classifiers. If an incoming packet
   logically matches a classifier, that classifier will assign a named
   service chain. If multiple classifiers match an incoming packet, the
   more specific classifier will win.

*This lab is less of a step-by-step guide and more intended as a
starting point for playing around with service chains and traffic
classifiers. The following are some ideas to get you started.*

Note: a hint is provided for each task below. For a challenge, cover up
the hint and try to build the traffic classification without help.

**Create a service chain that includes just the receive only and inline
layer 2 device, and a traffic classifier that matches this chain if the
source address is your client’s subnet.**

Verify that traffic is matching this chain by watching the debug log.
You can optionally insert tcpdump probes at the inbound (and outbound)
interfaces of the different security services to see if traffic is
correctly (or incorrectly) passing through them.

**Hint**:

-  Chain: ``Receive-only and layer 2 device``

-  Traffic classifier

   -  Phase: ``Normal``

   -  Protocol: ``All``

   -  Source: ``10.20.0.0/24``

   -  Destination (Address): ``0.0.0.0/0``

   -  Chain: ``<created chain>``

**Create a service chain that includes just the receive only and inline
layer 3 device, and a traffic classifier that matches the chain if the
traffic matches a specific URL category.**

SWG is provisioned in this lab and the URL category database has been
loaded. So for example, assign the *Financial\_Data\_and\_Services* URL
category and attempt to go to an online banking site.

**Hint**:

-  Chain: ``Receive-only and layer 3 device``

-  Traffic classifier:

   -  Phase: ``Normal``

   -  Protocol: ``All``

   -  Source: ``0.0.0.0/0``

   -  Destination (URLF – Category): ``Financial Data and Services``

   -  Chain: ``<created chain>``

**Create a service chain that includes the ICAP service, and a traffic
classifier that matches the chain if the traffic has a destination port
of ``443``.**

Here we’ll go to Eicar to see if we can download some sample malware,
and if the ICAP service will detect it. Navigate to
``http://www.eicar.org``, click on the ``DOWNLOAD ANTI MALWARE
TESTFILE`` link in the top right corner, click the ``DOWNLOAD`` link
on the left of the next page, and then scroll to the bottom of the
Download page to find the HTTP and HTTPS links for ``eicar.com``.
Click on the HTTPS link first. Then click on the HTTP link. If the test
was successful, you should see the ICAP service blocking page for the
HTTPS link, and the browser will (in error) try to download the file for
the HTTP link. This will prove that both the traffic classifier is
working as is decryption of traffic through the ICAP service.

**Hint**:

-  Chain: ICAP service

-  Traffic classifier:

   -  Phase: ``Normal``

   -  Protocol: ``All (or HTTP)``

   -  Source: ``0.0.0.0/0``

   -  Destination (Port): ``443``

   -  Chain: ``<created chain>``

**Create traffic classifiers that bypass SSL inspection for a specific
URL category and a separate unrelated hostname**

You’ll notice in the TCP Service Chain Classifiers of the SSL
Orchestrator Policies configuration that there are three built-in
service chains. The ‘All’ service chain includes all of the defined
services. The ‘Reject’ service chain causes traffic that matches this
classifier rule to be rejected. And the ‘Bypass’ service chain causes
matching traffic to bypass SSL processing. This traffic will not be
decrypted, and will flow directly to egress. With any (SSL) Bypass
operation you’ll want to use the ‘Pre Handshake’ phase in the classifier
rule. This phase makes its determination before full SSL processing is
enabled.

**Hint**:

-  Chain: ``none``

-  Traffic classifier 1:

   -  Phase: ``Pre-Handshake``

   -  Protocol: ``All``

   -  Source: ``0.0.0.0/0``

   -  Destination (URLF – Category): ``Financial Data and Services``

   -  Chain: ``Bypass``

-  Traffic classifier 2:

   -  Phase: ``Pre-Handshake``

   -  Protocol: ``All``

   -  Source: ``0.0.0.0/0``

   -  Destination (Name): ``www.bing.com``

   -  Chain: ``Bypass``
