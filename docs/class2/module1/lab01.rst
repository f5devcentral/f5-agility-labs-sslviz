.. role:: red
.. role:: bred

Lab 1.1: Review the lab environment and map out the services and endpoints
--------------------------------------------------------------------------

Review the “SSL Orchestrator Lab Environment” section above. This lab will
attach one of each type of security service (HTTP, ICAP, L2, L3, TAP) to SSLO
for an outbound forward proxy traffic flow. Afterwards, an internal client will
be able to access remote (Internet) resources through SSLO, providing
decrypted, inspectable traffic to the security services.

- The client is attached to a :red:`10.20.0.0/24` network and is assigned the
  IP :red:`10.20.0.60`. This network is attached to the BIG-IP 1.1 interface.

- The **L2 device** is an Ubuntu 14.04 LTS server configured to bridge its eth1
  and eth2 interfaces. Its inbound VLAN (traffic to it) is attached to the
  BIG-IP :red:`1.6` interface. Its outbound interface (traffic coming from it)
  is attached to the BIG-IP :red:`1.7` interface.

- The **L3 device** is an Ubuntu 14.04 LTS server configured to route between
  its eth1.10 and eth1.20 (tagged) interfaces. Its inbound VLAN (traffic to it)
  is attached to the BIG-IP :red:`1.3 (VLAN tag 30)` interface and has an IP of
  :red:`198.19.64.64/25`. Its outbound interface (traffic coming from it) is
  attached to the BIG-IP :red:`1.3 (VLAN tag 60)` interface and has an IP of
  :red:`198.19.64.130/25`. Its default gateway is :red:`198.19.64.245`, which
  will be a VLAN self-IP on the BIG-IP.

- The **TAP** device is an Ubuntu 14.04 LTS server configured with a single
  eth1 interface. That interface is attached to the BIG-IP :red:`1.4`
  interface.

- The **DLP/ICAP** device is an Ubuntu 14.04 LTS server configured with a
  single eth1 interface. That interface is attached to the BIG-IP :red:`1.5`
  interface and has an IP of :red:`10.70.0.10 and listening on port 1344`. The
  box is running c-icap and Squid/Clamav.

- The **Explicit Proxy device** is an Ubuntu 14.04 LTS server configured with
  Squid. Its interfaces are eth1.30 and eth1.40 (tagged). Its inbound VLAN
  (traffic to it) is attached to the BIG-IP :red:`1.3 (VLAN tag 110)` interface
  and has an IP of :red:`198.19.96.66/25`. Its outbound interface (traffic
  coming from it) is attached to the BIG-IP :red:`1.3 (VLAN tag 120)` interface
  and has an IP of :red:`198.19.96.136/25`. Its default gateway is
  :red:`198.19.96.245:red:`, which will be a VLAN self-IP on the BIG-IP.

- The outbound network is attached to the BIG-IP :red:`1.2` interface, in the
  :red:`10.30.0.0/24` subnet, and has a gateway of :red:`10.30.0.1`.

- In the lab, client inbound, Internet outbound, and DLP VLANs and self-IPs are
  already created.
