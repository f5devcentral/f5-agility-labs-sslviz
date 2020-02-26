SSL Orchestrator Lab Environment
================================

The following is a visual representation of this lab
environment. The numbers inside the right edge of the SSL Orchestrator
box indicate the port numbers assigned. The colored boxes to the right
of the services indicate a few product examples for each respective
service type.

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
     - admin:admin \| root:default
     -
   * - Interfaces
     - Client VLAN
     - 1.1
   * -
     - Outbound VLAN
     - 1.2
   * -
     - Explicit Proxy service
     - 1.6 (tagged)
   * -
     - TAP service
     - 1.7

.. list-table:: **Explicit proxy service**
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

.. list-table:: **Receive-only service**
   :header-rows: 0
   :widths: auto

   * - Login
     - root:default
   * - MAC Address
     - 12:12:12:12:12:12 (arbitrary if directly connected)

.. list-table:: **Active Directory Server and Client machine to test password-less authentication (Windows 2016 server)**
   :header-rows: 0
   :widths: auto

   * - Client VLAN address
     - 10.1.10.200
     -
   * - Login Credentials
     - **AD Group/Username**
     - **Password**
   * -
     - Accounting/ac-user1, 2 & 3
     - Same as username
   * -
     - Content-creators/cc-user1, 2 & 3
     - Same as username
   * -
     - CSO-Office/cs-user1, 2 & 3
     - Same as username
   * -
     - HR/hr-user1, 2 & 3
     - Same as username
   * -
     - IT/it-user1, 2 & 3
     - Same as username
   * -
     - Security-Admins/sa-user1, 2 & 3
     - Same as username

|
