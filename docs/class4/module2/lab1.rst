.. role:: red
.. role:: bred

Review the lab diagram and map out the services and endpoints
---------------------------------------------------------------------

.. note:: In this lab, there is a web server on the internal network (the
   client's network in this case) that external users want to get to.

- The external client is attached to a :red:`10.1.20.0/24` network and is
  assigned the IP :red:`10.1.20.55`. This network is attached to the BIG-IP
  :red:`1.2` interface.

- The web server is an Ubuntu 14.04 LTS server configured with Apache2 and
  PHP5, and listens on the following addresses:

  - :red:`10.1.10.90`
  - :red:`10.1.10.91`
  - :red:`10.1.10.92`

  .. note:: Each instance includes a simple text page that also shows
     which site was accessed. The pages are all (only) hosted via HTTPS on port 443.

- In lieu of a separate DNS server in the lab, the external client has static
  /etc/hosts entries that map the above addresses to different URLs:

  .. code-block:: bash

     10.1.10.90      test0.f5labs.com
     10.1.10.91      test1.f5labs.com
     10.1.10.92      test2.f5labs.com
     10.1.20.120     www.f5labs.com

  The first three addresses point the client *through* the SSLO
  inbound topology in gateway mode.

  The last address points the
  client *to* the SSLO inbound topology in application mode.

- The external client is also configured with a static route that
  points 10.1.10.0/24 destinations *through* the BIG-IP outbound-side
  self-IP. This is for lab testing in lieu of a separate router.

  .. code-block:: bash

     Kernel IP routing table

     Destination Gateway     Genmask       Flags Metric Ref Use Iface
     default     10.1.1.1    0.0.0.0       UG    0      0   0   eth0
     10.1.1.0    \*          255.255.255.0 U     0      0   0   eth0
     10.1.10.0   10.1.20.100 255.255.255.0 UG    0      0   0   eth1
     10.1.20.0   \*          255.255.255.0 U     0      0   0   eth1
     link-local  \*          255.255.0.0   U     1000   0   0   eth1

- A wildcard (:red:`\*.f5labs.com`) server certificate and private key have
  been installed on the SSL Orchestrator.


The external client has two options for accessing the internal websites: via
wildcard (0.0.0.0/0) gateway, and direct IP listener. The lab will explore both
options below.

.. note:: SSL Orchestrator sends all traffic through an inline layer 3 or HTTP
   device in the same direction - entering through the inbound interface. It is
   likely, therefore, that the layer 3 device may not be able to correctly
   route both outbound (forward proxy) and inbound (reverse proxy) traffic at
   the same time. For more details, see:
   `Appendix - Routing considerations for layer 3 devices <../appendix/appendix3.html>`_
