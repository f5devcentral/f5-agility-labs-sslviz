SSL Orchestrator Lab Environment
================================

The following is a visual representation of this lab environment. The numbers inside the right edge of the SSL Orchestrator box indicate the port numbers assigned. The colored boxes to the right of the services indicate a few product examples for each respective service type.

.. image:: images/labinfo-2.png
   :align: center

.. list-table:: **SSL Orchestrator**
   :header-rows: 0
   :widths: auto

   * - BIG-IP Management IP
     - 10.1.1.11
     -
   * - Gateway IP/DNS
     - 10.1.20.1
     -
   * - Login
     - admin:admin
     -
   * - 
     - root:default
     -
   * - Interfaces
     - Client VLAN
     - 1.1
   * -
     - Outbound VLAN
     - 1.2
   * -
     - Inline L2 service inbound
     - 1.4
   * -
     - Inline L2 service outbound
     - 1.5
   * -
     - Inline L3/HTTP services
     - 1.6 (tagged)
   * -
     - TAP service
     - 1.7

.. list-table:: **Windows 10 client**
   :header-rows: 0
   :widths: auto

   * - IP address
     - 10.1.10.50
     -
   * - Logins
     - **Username**
     - **Password**
   * -
     - F5LABS\\mike
     - agility
   * -
     - F5LABS\\jane
     - agility

.. list-table:: **Inline Layer 2 service**
   :header-rows: 0
   :widths: auto

   * - Login
     - student:agility

.. list-table:: **Inline Layer 3 service**
   :header-rows: 0
   :widths: auto

   * - Login
     - student:agility
     -
     -
   * - Interfaces
     - Inbound interface
     - 1.6 tag 10
     - 198.19.64.65/25
   * -
     - Outbound interface
     - 1.6 tag 20
     - 198.19.64.130/25

.. list-table:: **Explicit proxy (HTTP) service**
   :header-rows: 0
   :widths: auto

   * - Login
     - root:default
     -
     -
   * - Interfaces
     - Inbound interface
     - 1.6 tag 30
     - 198.19.96.66/25
   * -
     - Outbound interface
     - 1.6 tag 40
     - 198.19.96.131/25
   * - Services
     - Squid
     - Port 3128
     -
   * -
     - DansGuardian
     - Port 8080
     -

.. list-table:: **Receive-only (TAP) service**
   :header-rows: 0
   :widths: auto

   * - Login
     - root:default
   * - MAC Address
     - 12:12:12:12:12:12 (arbitrary if directly connected)