.. role:: red
.. role:: bred

SSL Orchestrator Lab Environment
================================

Accessing the Virtual Lab
-------------------------

If you are not familiar with the process for joining a training course, refer to:

- `How to join a training course <https://help.udf.f5.com/en/articles/3832165-how-to-join-a-training-course>`_
- `How to use the training course interface <https://help.udf.f5.com/en/articles/3832340-training-course-interface>`_

To access your lab and lookup the necessary IP addresses, you should have
received an email with your personal "Lab Portal Link". Once attached you
should have something similar to the following image. Highlighted is the "Lab
Guide" and the VM's you'll spend all of your time attached to.

.. NOTE::

   All of your lab exercise work will be done from a single jump host (accessed via Remove Desktop Protocol (RDP) client).
   
   You will not need to use SSH to access the UDF lab environment, so no SSH Key needs to be conffigured.

From the :bred:`DEPLOYMENT` tab, you will access the :bred:`DESKTOP-OUTBOUND` system over RDP. 
You can select the window resolution for the RDP session. An RDP file will be downloaded to your local
system and you will need to open it to connect.

|

.. image:: images/labinfo-2.png
   :align: center

Lab Details
-----------

Most of this lab can be accomplished by directly attaching to
the BIG-IP GUI.

.. IMPORTANT:: The lab environment for this guide has provided some
   prerequisite settings that you should be aware of. These are provided to
   make the lab simpler.

   The following information is based on a custom :bred:`UDF` blue print named
   :bred:`Agility 2020 - Essential SSL Visibility with SSLO`.

-  **Client side VLAN and subnet are pre-defined** - this is the VLAN
   that an internal client connects to for outbound traffic flows. SSLO
   does not define the client-side VLAN(s) and self-IP(s).

-  **Outbound side VLAN and subnet are pre-defined** - this is the VLAN
   that traffic egresses from SSLO to the Internet gateway. SSLO does
   not define the server-side VLAN(s) and self-IP(s).

-  **ICAP service VLAN and subnet are pre-defined** - SSLO does not
   define the networking for this service type, so it has been
   pre-created in this lab.

-  **CA certificate and private key are installed** - this is the CA
   certificate and private key that are used to re-issue (forge) remote
   server certificates to internal clients for outbound traffic flows.

-  **Server certificate and private key are installed** - for the
   inbound (reverse proxy) traffic flow use case, SSL traffic is
   terminated at the F5, and re-encrypted on the way to the internal
   application environment. A wildcard server certificate is installed
   to facilitate using any name under the ":red:`.f5labs.com`" sub-domain.

.. TIP:: It is a security best practice to isolate security devices
   within the protected network enclaves provided by SSLO. Customers will
   often desire NOT to move or change existing security services. However,
   while possible with SSLO 4.0 and beyond, passing this decrypted traffic
   to points on an existing network architecture could create multiple
   points of data exposure. Usernames, passwords, credit card numbers and
   other sensitive information could be exposed to other devices on that
   network. Each inline layer 3 security service definition includes an
   "Auto Manage" option. This option, enabled by default, provides internal
   network settings for security services to use, so that only the
   interface (and 802.1q VLAN tag as needed) is required to be defined for
   the inbound and outbound interfaces. Should customers opt to not follow
   security best practices, or simply need different networking settings,
   you can disable the Auto Manage option and define all of the required
   inbound and outbound networking setting manually.


.. list-table:: **SSL Orchestrator**
   :header-rows: 0
   :widths: auto

   * - BIG-IP SSLO Management IP
     - 10.1.1.x (UDF-managed)
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
     - ICAP service
     - 1.3
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
     - 1.6 tag 10
     - 198.19.64.65/25
   * -
     - Outbound interface
     - 1.6 tag 20
     - 198.19.64.130/25

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
     - Port 31281
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

.. list-table:: **ICAP service**
   :header-rows: 0
   :widths: auto

   * - Login
     - root:default
   * - IP Address:port
     - 10.1.30.50:1344
   * - REQ/RES URLs
     - /squidclamav

.. list-table:: **Internal web server**
   :header-rows: 0
   :widths: auto

   * - Login
     - root:default
   * - IP Addresses (\*.f5labs.com)
     - 10.1.10.90

       10.1.10.91

       10.1.10.92 (Apache2 instances listening on HTTPS port 443)

       10.1.10.93

       10.1.10.94

.. list-table:: **Outbound client**
   :header-rows: 0
   :widths: auto

   * - Login
     - student:agility
   * - IP address
     - 10.1.10.50 (RDP and SSH)

.. list-table:: **Inbound client**
   :header-rows: 0
   :widths: auto

   * - Login
     - student:agility
   * - IP address
     - 10.1.20.55 (RDP and SSH)

|

The following is a visual representation of this lab
environment. The numbers inside the right edge of the SSL Orchestrator
box indicate the port numbers assigned. The colored boxes to the right
of the services indicate a few product examples for each respective
service type.

.. image:: images/labinfo-3.png
   :align: center
