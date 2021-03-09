.. role:: red
.. role:: bred

Login and review the UDF lab hosts and endpoints
===============================================================================

If needed, review the previous section
`SSL Orchestrator Lab Environment <../labinfo.html>`_.

-  Using your web browser (Chrome preferred), open a :red:`TMUI (HTTPS)` session 
   to the :red:`BIGIP SSLO Primary` component.
   
-  Login as :red:`admin` with password :red:`admin`.

.. note:: There are no additional steps that need to be taken by the student before proceeding to the next section.  The information below is intended to provide additional context regarding how the UDF lab hosts are connected and how they relate to each other.

-  The **Desktop-Outbound** client is attached to a :red:`10.1.10.0/24` network
   and is assigned the IP :red:`10.1.10.50`. This network is attached to the
   BIG-IP :red:`1.1` interface.

-  The **L2 device** is an Ubuntu 14.04 LTS server configured to bridge its eth1
   and eth2 interfaces. Its inbound VLAN (traffic to it) is attached to the
   BIG-IP :red:`1.4` interface. Its outbound interface (traffic coming from it)
   is attached to the BIG-IP :red:`1.5` interface.

-  The **L3 device** is an Ubuntu 14.04 LTS server configured to route between
   its eth1.10 and eth1.20 (tagged) interfaces. Its inbound VLAN (traffic to it)
   is attached to the BIG-IP :red:`1.3 (VLAN tag 10)` interface and has an IP of
   :red:`198.19.64.65/25`. Its outbound interface (traffic coming from it) is
   attached to the BIG-IP :red:`1.3 (VLAN tag 20)` interface and has an IP of
   :red:`198.19.64.130/25`. Its default gateway is :red:`198.19.64.245`, which
   will be a VLAN self-IP on the BIG-IP.

-  The **TAP** device is an Ubuntu 14.04 LTS server configured with a single
   eth1 interface. That interface is attached to the BIG-IP :red:`1.7`
   interface.

-  The **DLP/ICAP** device is an Ubuntu 14.04 LTS server configured with a
   single eth1 interface. That interface is attached to the BIG-IP :red:`1.3`
   interface and has an IP of :red:`198.19.97.50 and listening on port 1344`. The
   box is running c-icap and Squid/Clamav.

-  The **Explicit Proxy device** is an Ubuntu 14.04 LTS server configured with
   Squid. Its interfaces are eth1.30 and eth1.40 (tagged). Its inbound VLAN
   (traffic to it) is attached to the BIG-IP :red:`1.6 (VLAN tag 30)` interface
   and has an IP of :red:`198.19.96.66/25`. Its outbound interface (traffic
   coming from it) is attached to the BIG-IP :red:`1.6 (VLAN tag 40)` interface
   and has an IP of :red:`198.19.96.131/25`. Its default gateway is
   :red:`198.19.96.245`, which will be a VLAN self-IP on the BIG-IP.

-  The outbound network is attached to the BIG-IP :red:`1.2` interface, in the
   :red:`10.1.20.0/24` subnet, and has a gateway of :red:`10.1.20.1`.

.. note:: In this lab, the client inbound, Internet outbound, and DLP VLANs and
   self-IPs are already created.
