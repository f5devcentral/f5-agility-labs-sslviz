SSL Orchestrator Lab Environment
================================

The lab environment for this guide has provided some prerequisite settings that
you should be aware of. These are provided to make the demo simpler. All of the
following would need to be configured manually in another environment.

- **Client side VLAN and subnet are defined** – this is the VLAN that an
  internal client connects to for outbound traffic flows. SSLO does not define
  the client-side VLAN(s) and self-IP(s). A web server also exists on the
  client side VLAN to facilitate an inbound (reverse proxy) use case – external
  client to an internal set of websites.

- **Outbound side VLAN and subnet are defined** – this is the VLAN that traffic
  egresses from SSLO to the Internet gateway. SSLO does not define the
  server-side VLAN(s) and self-IP(s).

- **ICAP service VLAN and subnet are defined** – SSLO does not define the
  networking for this service type, so it has been pre-created in this lab.

- **CA certificate and private key are installed** – this is the CA certificate
  and private key that are used to re-issue (forge) remote server certificates
  to internal clients for outbound traffic flows.

- **Server certificate and private key are installed** – for the inbound
  (reverse proxy) traffic flow use case, SSL traffic is terminated at the F5,
  and re-encrypted on the way to the internal application environment. A
  wildcard server certificate is installed to facilitate using any name under
  the "*f5demolabs.com*" sub-domain.

.. note:: It is a security best practice to isolate security devices within the
   protected network enclaves provided by SSLO. Customers will often desire NOT
   to move or change existing security services. However, while possible with
   SSLO 4.0 and beyond, passing this decrypted traffic to points on an existing
   network architecture could create a provide multiple points of data
   exposure. Usernames, passwords, credit card numbers and other sensitive
   information could be exposed to other devices on that network. Each inline
   layer 3 security service definition includes an "Auto Manage" option. This
   option, enabled by default, provides internal network settings for security
   services to use, so that only the interface (and 802.1q VLAN tag as needed)
   is required to be defined for the inbound and outbound interfaces. Should
   customers opt to not follow security best practices, or simply need
   different networking settings, you can disable the Auto Manage option and
   define all of the required inbound and outbound networking setting manually.

.. list-table:: **SSL Orchestrator**
   :header-rows: 0
   :widths: auto

   * - BIG-IP Management IP
     - 10.10.0.110
     - 
   * - Gateway IP/DNS
     - 10.30.0.1
     - 
   * - Login
     - admin:admin \| root:default
     -
   * - Interfaces
     - Client VLAN
     - 1.1
   * - 
     - Outbound VLAN
     - 1.2
   * - 
     - Inline L3/HTTP services
     - 1.3 (tagged)
   * - 
     - TAP service
     - 1.4
   * - 
     - ICAP service
     - 1.5
   * - 
     - Inline L2 service inbound
     - 1.6
   * - 
     - Inline L2 service outbound
     - 1.7

.. list-table:: **Inline layer 2 service**
   :header-rows: 0
   :widths: auto

   * - Login
     - student:agility

.. list-table:: **Inline layer 3 service**
   :header-rows: 0
   :widths: auto   

   * - Login
     - student:agility
     -
     -
   * - Interfaces
     - Inbound interface
     - 1.3 tag 50
     - 198.19.64.64/25
   * - 
     - Outbound interface
     - 1.3 tag 60
     - 198.19.64.130/25

.. list-table:: **Explicit proxy service**
   :header-rows: 0
   :widths: auto   

   * - Login
     - student:agility
     -
     -
   * - Interfaces
     - Inbound interface
     - 1.3 tag 110
     - 198.19.96.66/25
   * - 
     - Outbound interface
     - 1.3 tag 120
     - 198.19.96.136/25
   * - Service
     - Squid
     - Port 31281
     - 

.. list-table:: **Receive-only service**
   :header-rows: 0
   :widths: auto

   * - Login
     - student:agility
   * - MAC Address
     - 12:12:12:12:12:12 (arbitrary if isolated)

.. list-table:: **ICAP service**
   :header-rows: 0
   :widths: auto

   * - Login
     - student:agility
   * - IP Address:port
     - 10.70.0.10:1344
   * - REQ/RES URLs
     - /squidclamav

.. list-table:: **Internal web server**
   :header-rows: 0
   :widths: auto   

   * - Login
     - student:agility
   * - IP Addresses (\*.f5demolabs.com)
     - 10.20.0.90
   * - 
     - 10.20.0.91
   * - 
     - 10.20.0.92 (Apache2 instances listening on HTTPS port 443)

.. list-table:: **Outbound client**
   :header-rows: 0
   :widths: auto

   * - Login
     - student:agility
   * - IP address
     - 10.20.0.60 (RDP and SSH)

.. list-table:: **Inbound client**
   :header-rows: 0
   :widths: auto

   * - Login
     - student:agility
   * - IP address
     - 10.30.0.70 (RDP and SSH)
