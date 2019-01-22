.. role:: red
.. role:: bred

Lab 1.2: Fulfill the SSL Orchestrator prerequisites
---------------------------------------------------

There are a number of objects that SSL Orchestrator does not create and expects
to exist before deploying the iApp. You must create the following objects
before starting the iApp:

- **Import the CA certificate and private key** – in order to terminate and
  re-encrypt outbound SSL traffic, SSL Forward Proxy must re-issue, or rather
  "forge" a new server certificate to the client. In order to perform this
  re-issuance process, the BIG-IP must possess a certificate authority (CA)
  certificate and associated private key. :red:`This lab environment already
  has a subordinate CA certificate and private key installed`.

- **Create the client inbound VLAN and self-IP** – create the VLAN and self-IP
  that connects the client to the BIG-IP. In this lab that’s the
  :red:`10.20.0.0/24` subnet and interface :red:`1.1` on the BIG-IP. This lab
  environment already has this VLAN and self-IP created.

- **Create the Internet outbound VLAN and self-IP** – create the VLAN and
  self-IP that connects the BIG-IP to the outbound Internet router. In this lab
  that’s the :red:`10.30.0.0/24` subnet and interface :red:`1.2` on the BIG-IP.
  :red:`This lab environment already has this VLAN and self-IP created`.

- **Create the DLP VLAN and self-IP** – if it is desired to isolate the
  DLP/ICAP device, create the VLAN and self-IP that connects the DLP device to
  the BIG-IP. In this lab that’s the :red:`10.70.0.0/24` subnet and interface
  :red:`1.5` on the BIG-IP. The DLP security device is listening on
  :red:`10.70.0.10` and ICAP is listening on port :red:`1344`. :red:`This lab
  environment already has this VLAN and self-IP created`.

- **Create the default internet route for outbound traffic** – the iApp
  provides an option to leverage a defined gateway pool or use the system
  default route. If a gateway pool is not used, they system route table will
  need to have a default route used to reach Internet destination. :red:`We’ll
  use a gateway pool defined within SSLO`.

.. note:: As a general rule, avoid using names with dashes (ex. sslo-demo-1)
   while creating objects in SSL Orchestrator. Underscores (ex. sslo_demo_1)
   and camel-casing (ex. ssloDemo1) are preferred.
