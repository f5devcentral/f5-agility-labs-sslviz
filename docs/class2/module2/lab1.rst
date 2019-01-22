.. role:: red
.. role:: bred

Lab 2.1: Review the lab diagram and map out the services and endpoints
----------------------------------------------------------------------

Specifically, note that in this lab there is a web server on the internal
network (the client’s network in this case) that external users want to get to.
An external client desktop exists on the external/outbound network, that
accesses these resources through SSLO.

- The external client is attached to a *10.30.0.0/24* network and is assigned
  the IP *10.30.0.70*. This network is attached to the BIG-IP 1.2 interface.

- The web server is an Ubuntu 14.04 LTS server configured with Apache2 and
  PHP5, and listens on five addresses:

  - 10.20.0.90

  - 10.20.0.91

  - 10.20.0.92

  .. note:: Each instance includes a simple Apache2 text page that also shows
     which site was accessed. The pages are all (only) hosted via HTTPS port 443.

- In lieu of a separate DNS server in the lab, the external client has static
  /etc/hosts entries that map the above addresses to the following URLs,
  respectively:

  - test0.f5demolabs.com

  - test1.f5demolabs.com

  - test3.f5demolabs.com

- A wildcard (\*.f5demolabs.com) server certificate and private key have been
  installed on the SSL Orchestrator.

The external client has two options for accessing the internal websites: via
wildcard (0.0.0.0/0) gateway, and direct IP listener. The lab will explore both
options below.

.. note:: SSL Orchestrator sends all traffic through an inline layer 3 or HTTP
   device in the same direction – entering through the inbound interface. It is
   likely, therefore, that the layer 3 device may not be able to correctly
   route both outbound (forward proxy) and inbound (reverse proxy) traffic at
   the same time. Please see the appendix, "Routing considerations for layer 3
   devices" for more details.
