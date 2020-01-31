SSL ORCHESTRATOR LAB ENVIRONMENT
================================

The lab environment for this guide has provided some prerequisite
       settings that you should be aware of. These are provided to make the
       demo simpler. All of the following would need to be configured manually
       in another environment.

       -  **Client side VLAN and subnet are pre-defined** – this is the VLAN
              that an internal client connects to for outbound traffic flows.
              SSLO does not define the client-side VLAN(s) and self-IP(s). A
              web server also exists on the client side VLAN to facilitate an
              inbound (reverse proxy) use case – external client to an internal
              set of websites.

       -  **Outbound side VLAN and subnet are pre-defined** – this is the VLAN
              that traffic egresses from SSLO to the Internet gateway. SSLO
              does not define the server-side VLAN(s) and self-IP(s).

       -  **ICAP service VLAN and subnet are pre-defined** – SSLO does not
              define the networking for this service type, so it has been
              pre-created in this lab.

       -  **Required objects and Access policy for password-less authentication**
              have been pre-created – These objects are created using the APM
              module of F5. To maintain the focus on SSLO, these have been
              pre-created and provided for easy configuration for SSLO. In a
              production environment these will have to be created from
              scratch.

       -  **CA certificate and private key are installed** – this is the CA
              certificate and private key that are used to re-issue (forge)
              remote server certificates to internal clients for outbound
              traffic flows.

       -  **Server certificate and private key are installed** – for the
              inbound (reverse proxy) traffic flow use case, SSL traffic is
              terminated at the F5, and re-encrypted on the way to the internal
              application environment. A wildcard server certificate is
              installed to facilitate using any name under the
              “.\ *f5labs.com*\ ” sub-domain.



       .. note:: It is a security best practice to isolate security devices
              within the protected network enclaves provided by SSLO. Customers will
              often desire NOT to move or change existing security services. However,
              while possible with SSLO 4.0 and beyond, passing this decrypted traffic
              to points on an existing network architecture could create multiple
              points of data exposure. Usernames, passwords, credit card numbers and
              other sensitive information could be exposed to other devices on that
              network. Each inline layer 3 security service definition includes an
              “Auto Manage” option. This option, enabled by default, provides internal
              network settings for security services to use, so that only the
              interface (and 802.1q VLAN tag as needed) is required to be defined for
              the inbound and outbound interfaces. Should customers opt to not follow
              security best practices, or simply need different networking settings,
              you can disable the Auto Manage option and define all of the required
              inbound and outbound networking setting manually.

+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |     BIG-IP management IP   |     10.1.1.x (UDF-managed)                                       |                                  |              |                        |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |     Gateway IP/DNS         |     10.1.20.1                                                    |                                  |              |                        |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |     Login                  |     admin:admin \| root:default                                  |                                  |              |                        |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |                            |                                                                  |     Client VLAN                  |              |     1.1                |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|     **SSL Orchestrator**         |                            |                                                                  |     Outbound VLAN                |              |     1.2                |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |     Interfaces             |     TAP Service                                                  |                                  |     1.3      |                        |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |                            |                                                                  |     Inline L3/HTTP services      |              |     1.6 (tagged)       |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+


+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |     Login                  |     root:default                                                 |                                  |              |                        |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|     **Explicit proxy service**   |     Interfaces             |     Inbound interface                                            |                                  | 1.6 tag 30   |     198.19.96.66/25    |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |                            |     Outbound interface                                           |                                  | 1.6 tag 40   |     198.19.96.131/25   |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |     Services               |     Squid                                                        |                                  | Port 3128    |                        |
+                                  +----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+
|                                  |                            |     DansGuardian                                                 |                                  | Port 8080    |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+


+----------------------------------+----------------------------+------------------------------------------------------------------+
|     **Receive-only service**     |     Login                  |     root:default                                                 |
+                                  +----------------------------+------------------------------------------------------------------+
|                                  |     MAC address            |     12:12:12:12:12:12 (arbitrary if directly connected)          |
+----------------------------------+----------------------------+------------------------------------------------------------------+


+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+------------------------+
|                                                                                                              | AD server management IP       |     10.1.1.x (UDF-managed)         |                        |
+                                                                                                              +-------------------------------+------------------------------------+------------------------+
|                                                                                                              | Client VLAN address           |     10.1.10.200                    |                        |
+                                                                                                              +-------------------------------+------------------------------------+------------------------+
|                                                                                                              | Login Credentials             |     Various as shown below         |                        |
+                                                                                                              +                               +------------------------------------+------------------------+
|                                                                                                              |                               |  **AD Group/username**             | **Password**           |
+                                                                                                              +                               +------------------------------------+------------------------+
|     **Active Direct Server and Client machine to test password-less authentication (Windows 2016 server)**   |                               |  Accounting/ac-user1, 2 & 3        | Same as username       |
+                                                                                                              +                               +------------------------------------+------------------------+
|                                                                                                              |                               |  Content-creators/cc-user1, 2 & 3  | Same as username       |
+                                                                                                              +                               +------------------------------------+------------------------+
|                                                                                                              |                               |  CSO-Office/cs-user1, 2 & 3        | Same as username       |
+                                                                                                              +                               +------------------------------------+------------------------+
|                                                                                                              |                               |  HR/hr-user1, 2 & 3                | Same as username       |
+                                                                                                              +                               +------------------------------------+------------------------+
|                                                                                                              |                               |  IT/it-user1, 2 & 3                | Same as username       |
+                                                                                                              +                               +------------------------------------+------------------------+
|                                                                                                              |                               |  Security-Admins/sa-user1, 2 & 3   | Same as username       |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+------------------------+

