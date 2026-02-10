.. role:: red
.. role:: bred

Appendix 7 - L2 Mode Without Virtual Wire Support
=================================================

True layer 2 topology support in SSL Orchestrator is a function of a Broadcom
chipsets available in iSeries i5000 appliances and above. This chipset is not
available in i2000, i4000, Bourne-series platforms, Viprion, or vCMP instances
(regardless of platform). It is possible, however, to modify SSLO to support a
software-based layer 2 configuration. In a layer 2 topology, the client and
server sides of the F5, while on separate physical interfaces, share the same
IP subnet. A VLAN group is required to bridge the interfaces, allowing ARP and
other routing protocol traffic to flow through, while the SSLO listeners
process TCP and UDP traffic. The Transparent Nexthop setting, included in the
SSLO license, then copies the layer 2 headers across the proxy environment. The
following steps detail that configuration for SSLO 5.0.

.. attention:: **In preparation for a layer 2 topology environment, the
   following prerequisites are required:**

   - The BIG-IP must have defined, separate VLANs for the client-side and
     server-side networks. These VLAN's must be on the same IP subnet.
   - The BIG-IP must NOT have self-IPs configured on these VLANs.

Configure the software-based layer 2 topology
---------------------------------------------

#. Delete (or do not create) client-side and server-side VLAN self-IPs on the
   BIG-IP.
#. Create a VLAN group combining the client-side and server-side VLANs, with
   Transparent mode, and “Bridge All Traffic” enabled. At this point the client
   should be able to ping the gateway and access server side (i.e. Internet
   resources), all flowing through the VLAN group. The next step is to enable
   SSLO processing.

   .. caution:: Do not switch between Translucent and Transparent mode in the
      VLAN group settings. Translucent mode performs a bit-flip on the
      destination MAC passing through the VLAN group, which is both
      incompatible with SSLO, and can be incorrectly cached by upstream routing
      devices.

#. Enable VIP traffic processing in the presence of a VLAN group. By default, a
   VLAN group will take precedence over LTM virtual servers. The following TMSH
   commands allow the SSLO virtual servers to capture TCP and UDP traffic,
   while ARP and other routing protocol traffic flows through the VLAN group.

   .. code-block:: bash

      tmsh modify sys db vlangroup.forwarding.override value disable
      tmsh save sys config

#. Process an SSLO **outbound proxy topology** workflow. Follow these steps to
   configure SSLO processing for outbound traffic. Full details on the SSL
   Orchestrator configuration are available in the respective deployment guide

   a. Topology Properties
      
      - Protocol: Any
      - Topology: L3 Outbound
 
   #. System Settings - nothing required, additional logging optional.
   #. SSL Configurations - define as required for outbound SSL inspection.
   #. Services List - add security services as required.
   #. Service Chain - add service chains as required.
   #. Security Policy - create an outbound security policy as required.
   #. Interception Rules

      - Rule Type: Default
      - VLANs: client-side VLAN

   #. Deploy

#. Disable strictness on the new topology. Click the lock icon (to unlock) on
   the Topology tab.

#. In the BIG-IP UI, under Local Traffic -> Virtual Servers, edit the -in-t-,
   -in-u-, and -ot-virtual servers. In the Transparent Nexthop setting, apply
   the VLAN group. If enabled, also add this setting to any FTP, SMTP, IMAP or
   POP3 virtual servers.

   .. important:: Editing the topology settings or Interception Rules in the
      SSLO UI will override the Transparent Nexthop settings in the LTM virtual
      servers.

#. Optionally create any required SSLO L3 **inbound topology** workflows,
   disable strictness on the topology, then apply the Transparent Nexthop
   settings to the respective LTM virtual servers.

   a. Topology Properties

      - Protocol: TCP
      - Topology: L3 Outbound
        
        .. attention:: This is not a typo.  For "inbound topology" the "L3
           Outbound" topology must be selected.

   #. SSL Configurations – define as required for outbound SSL inspection.
   #. Services List – add new security services as required, or re-use existing
      services.
   #. Service Chain – add new service chains, or re-use existing service
      chains.
   #. Security Policy – create an inbound security as required. Inbound traffic
      generally does not require categorization or additional intercept/bypass
      rules, so it is usually sufficient to strip the inbound security policy
      down to just the ‘All’ rule that intercepts and sends to the define
      service chain.
   #. Interception Rules

      - Source: 0.0.0.0/0 (or as required)
      - Destination: 0.0.0.0/0 (this is an L2 configuration, so nothing else
        makes sense)
      - Port: 443 (or as required)
      - VLANs: ingress VLAN
      - L7 Profile Type: HTTP (or as required)
      - L7 Profile: /Common/http (or as required)

   #. Deploy

Verify correct SSLO traffic processing
--------------------------------------

Perform any or more of the following steps:

- Validate that the client is able to access resources on the other side of the
  BIG-IP. If remote resources are accessible, inspect the server certificate in
  the browser to view the issuer.
- Monitor the APM log in debug mode. This will indicate if SSLO is processing
  traffic.
- Monitor the inbound or outbound interfaces of an inline service. All traffic
  to is should be decrypted, so a simple tcpdump would display clear text
  traffic:

  .. code-block:: bash

     tcpdump -lnni eth1-Xs0

Testing a software L2 solution
------------------------------

An L2 deployment topology (software or hardware) basically works like this:

- A VLAN group defines a "bridged" interface through which all traffic passes
  across the BIG-IP. Normally this would override any VIP listeners, except
  that the vlangroup.forwarding.override DB key (set to disabled) overrides
  this behavior allowing more specific virtual servers to process traffic.
- In an L2 topology, both sides of the F5 are on the same subnet, such that the
  client can ARP and ping the gateway (next hop), which naturally passes
  through the VLAN group bridge.
- In an L2 SSLO topology, There are no client/server-facing self-IPs on the F5.
  A client-facing TCP virtual server processes all TCP traffic. Traffic
  arriving at the TCP VIP contains the true destination IP and the MAC address
  of the next hop (gateway).
- SSLO handles encryption and shuffles decrypted traffic through the service
  chain. Virtual wire and Transparent Nexthop both function to then insert
  (copy) the L2 headers from the client-side packets to the server-side.
  Traffic arriving at the next hop correctly contains the true destination IP
  and MAC of the next hop.

The primary differences between hardware L2 (virtual wire) and software L2
(Transparent Nexthop) are:

a. The type and number of L2 headers copied, and
b. The type of VLAN group and objects created to support virtual wire.

For most situations, however, software L2 is adequate. In order to demonstrate
software L2, either follow the guidance above to create the configuration, or
one exists in the "SSLO 5.0 Software L2 Demo" UDF blueprint. The following
instructions assume the UDF blueprint:

- SSH or RDP to the outbound client. The client is at 10.1.20.50, and should be
  able to ping the gateway at 10.1.20.1 through the VLAN group bridge. Assuming
  that works, a client browser should be able to navigate to external sites.
- SSH or console to the Inline L2 device (simulated FireEye). Tcpdump on its
  eth1 interface (tcpdump -lnni eth1 -Xs0 not icmp and not icmp6). Generate
  HTTPS traffic on the client to see decrypted traffic in this capture.
  able to ping the webservers at 10.1.20.90-92. Assuming that works, a client
  browser should be able to navigate to one of the internal test URLs:

  - test0.f5labs.com
  - test1.f5labs.com
  - test2.f5labs.com

- SSH or console to the webserver and tcpdump on its eth1 interface (tcpdump
  -lnni eth1 not icmp and not arp). This traffic is re-encrypted so you won’t
  see clear text.
