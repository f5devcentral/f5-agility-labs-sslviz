.. role:: bred

SSL Orchestrator Lab Environment
================================

The following is a visual representation of this lab environment. The numbers inside the right edge of the SSL Orchestrator box indicate the port numbers assigned. The colored boxes to the right of the services indicate a few product examples for each respective service type.

.. image:: images/labinfo-1.png
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
     - Inline L3, HTTP, and ICAP services
     - 1.3 (tagged)
   * -
     - TAP service
     - 1.6

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
     - 1.3 tag 60
     - 198.19.64.7/25
   * -
     - Outbound interface
     - 1.3 tag 70
     - 198.19.64.245/25
   * - Services
     - NGFW
     - 
     - 198.19.64.30/25

.. list-table:: **Explicit proxy (HTTP) service**
   :header-rows: 0
   :widths: auto

   * - Login
     - root:default
     -
     -
   * - Interfaces
     - Inbound interface
     - 1.3 tag 30
     - 198.19.96.7/25
   * -
     - Outbound interface
     - 1.3 tag 40
     - 198.19.96.245/25
   * - Services
     - Squid
     - Port 3128
     - 198.19.96.30

.. list-table:: **ICAP service**
   :header-rows: 0
   :widths: auto

   * - Login
     - root:default
     -
     -
   * - Interface
     - Inbound interface
     - 1.3 tag 50
     - 198.19.97.1/25
   * - Services
     - Squid ClamAV
     - Port 1433
     - 198.19.97.50/25

       Request Modification URI Path: /avscan

       Response Modification URI Path: /avscan

       Preview Max Length: 1048576


.. list-table:: **Receive-only (TAP) service**
   :header-rows: 0
   :widths: auto

   * - Login
     - root:default
   * - MAC Address
     - 12:12:12:12:12:12 (arbitrary if directly connected)