.. role:: red
.. role:: bred

Lab Environment Details
================================================================================

.. note::

   This lab guide and corresponding UDF lab blueprint are prepared for **BIG-IP Next SSL Orchestrator**, using a consolidated services lab architecture. All security services are consolidated into to a single Ubuntu server instance using a Docker Compose environment.

|

Network Diagram
--------------------------------------------------------------------------------

Here is a visual representation of the virtual lab environment. The numbers inside the right edge of the SSL Orchestrator box indicate the port numbers and VLAN tags (if applicable). The colored boxes to the right of the services respresent some product examples for each respective service type.

The first interface is connected to the client-facing VLAN. The last interface is connected to the Internet-facing VLAN. One of the tagged interfaces connects to the application server VLAN. The remaining interfaces are connected to various types of security services: L2, L3, HTTP, ICAP, and passive Tap. The SSL Orchestrator management interface is not shown.

.. image:: ./images/labinfo-1.png
   :align: left


Virtual Lab Infrastructure Details (and Credentials)
--------------------------------------------------------------------------------

The lab environment for this guide includes some prerequisite configuration settings that you
should be aware of. These are provided to simplify this course. If you wish to use
this lab guide with your own environment, please ensure that you create these objects in advance.

-  **Client side VLAN and subnet are pre-defined** - This is the VLAN
   that a client connects to for traffic flows. SSL Orchestrator does
   not define the client-side VLAN(s) and self-IP(s).

-  **Server side VLAN and subnet are pre-defined** - This is the VLAN
   that traffic egresses from the F5 BIG-IP to the web servers. SSL
   Orchestrator does not define the server-side VLAN(s) and self-IP(s).
   Consequently, the consolidated architecture will use the same
   interface on separate tagged VLANs to establish connectivity to the
   L3, HTTP, and ICAP inspection services.

-  **TAP service VLAN is pre-defined** - This is the VLAN that traffic egresses from
   the F5 BIG-IP to the TAP inspection service.

-  **CA certificate and private key are installed** - This is the CA
   certificate and private key that are used to re-issue (forge) remote
   server certificates to internal clients for outbound traffic flows.

-  **Server certificate and private key are installed** - For the
   inbound (reverse proxy) traffic flow use case, SSL traffic is
   terminated at the F5, and re-encrypted on the way to the internal
   application environment. A wildcard server certificate is installed
   to facilitate using any name under the "*f5labs.com*"
   sub-domain.

.. note::

   It is a security best practice to isolate security
   devices within the protected network enclaves provided by SSL
   Orchestrator. Administrators will often desire NOT to move or change
   existing security services. However, while possible, passing this
   decrypted traffic to points on an existing network architecture could
   create multiple points of data exposure. Usernames, passwords, credit
   card numbers and other personally identifiable information (PII) could be exposed to
   other devices on that network. It is thus recommended that security
   devices exist in a "private enclave" local to the BIG-IP Next
   instance(s). Please keep this in mind when defining the network
   settings for the inspection services.*

|

.. note::

   Special note about BIG-IP Next and Central Manager: The F5 Central Manager (CM) employs a "fleet
   management" configuration paradigm for BIG-IP Next and is the "source-of-truth" for all
   configuration state. In most cases, objects created in CM (like iRules) are only deployed to a
   Next instance when they are associated to an application. With respect to SSL Orchestrator, this
   also applies to service chains and traffic policies. The exemption to this is inspection
   services. While inspection services can be saved to CM and deployed later, they are generally
   deployed direct to an instance on creation, irrespective of applications, as they have network
   attributes that are typically specific to a BIG-IP Next instance. This will be made evident in
   the upcoming labs.


The following tables provide device/service network configuration details. Login credentials are also provided for use as directed in the lab exercises.


**F5 BIG-IP Next Central Manager**

.. list-table:: 
   :header-rows: 1
   :widths: auto

   * - Username
     - Password
     - Description
   * - admin
     - Welcome123!
     - Admin account

|

.. list-table:: 
   :header-rows: 1
   :widths: auto

   * - Interface/Resource
     - IP
     - Notes
   * - Management IP
     - 10.1.1.6/24
     - Management VLAN
   * - System DNS
     - 10.1.1.1
     - 
   * - Gateway IP/DNS
     - 10.1.1.1
     - 

|

**F5 BIG-IP Next SSL Orchestrator**

.. list-table:: 
   :header-rows: 1
   :widths: auto

   * - Username
     - Password
     - Description
   * - admin
     - Welcome123!
     - Admin account (pre-onboarding)

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Interface
     - IP
     - Description
   * - Management
     - 10.1.1.7/24
     - Management VLAN
   * - 1.1
     - 10.0.10.7/24
     - Client-Side VLAN (Ubuntu-Client)
   * - 1.2 (Tag 30)
     - 198.19.96.7/25
     - Inline HTTP service - Inbound
   * - 1.2 (Tag 40)
     - 198.19.96.245/25
     - Inline HTTP service - Outbound
   * - 1.2 (Tag 50)
     - 198.19.97.7/25
     - ICAP Service - Inbound/Outbound
   * - 1.2 (Tag 60)
     - 198.19.64.7/25
     - Inline L3 service - Inbound
   * - 1.2 (Tag 70)
     - 198.19.64.245/25
     - Inline L3 service - Outbound
   * - 1.2 (Tag 80)
     - 192.168.100.7/24
     - Server-side (lab webservers)
   * - 1.3
     - 10.1.30.7/24
     - TAP service - Inbound
   * - 1.4
     - Future (10.1.40.0/24)
     - Inline L2 service - Inbound
   * - 1.5
     - Future (10.1.50.0/24)
     - Inline L2 service - Outbound
   * - 1.6
     - Future (10.1.60.0/24)
     - Internet

|

**Client (inbound/outbound)**

.. list-table::
   :header-rows: 1
   :widths: 200 300 300

   * - Interfaces
     - IP Address
     - VLAN
   * - eth1
     - 10.1.10.50
     - Client-Side VLAN

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Access
     - Username
     - Password
   * - WEB SHELL
     - N/A
     - N/A
   * - RDP (XRDP)
     - user
     - user

|

**Ubuntu Server (Consolidated Services)**

.. list-table:: 
   :header-rows: 1
   :widths: 200 300 300

   * - Interfaces
     - IP Address
     - VLAN
   * - eth1
     - 10.1.20.50
     - Inline L3 services
   * - eth2
     - 10.1.30.50
     - TAP service
   * - eth3
     - 10.1.40.50
     - Inline L2 service - Inbound
   * - eth4
     - 10.1.50.50
     - Inline L2 service - Outbound

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Access
     - Username
     - Password
   * - WEB SHELL
     - N/A
     - N/A
   * - WEBRDP (Client Desktop Access)
     - user
     - user

The **WebRDP** service leverages an instance of Guacamole running on the Ubuntu Server. This acts as a web-based RDP client that connects to the Client VM.

|

**Inline Layer 2 Service**

.. list-table::
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host  -- ens8 and ens9

       br0 (bridge) tied to ens8 and ens9 interfaces on host
   * - Services
     - Suricata

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Traffic Flow
     - BIG-IP Interface
   * - Inbound
     - Future
   * - Outbound
     - Future

|

**Inline Layer 3 Service**

.. list-table::
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.60 and ens6.70
   * - Services
     - Firewall
   * - Access
     - $ ``docker exec -it layer3 /bin/bash``

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Traffic Flow
     - BIG-IP Interface
     - Service IP Address
   * - Inbound
     - 1.2 tag 60
     - 198.19.64.30/25
   * - Outbound
     - 1.2 tag 70
     - 198.19.64.130/25

|

**HTTP Explicit Proxy Service**

.. list-table::
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.30 and ens6.40
   * - Services
     - Squid - Port 3128
   * - Access
     - $ ``docker exec -it explicit-proxy /bin/bash``

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Traffic Flow
     - BIG-IP Interface
     - Service IP Address
   * - Inbound
     - 1.2 tag 30
     - 198.19.96.30/25
   * - Outbound
     - 1.2 tag 40
     - 198.19.96.130/25


|

**TAP Service**

.. list-table::
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens7

       ens7 interface tied to tap service on host
   * - Services
     - Passive TAP

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Traffic Flow
     - BIG-IP Interface
     - MAC Address
   * - In/Out
     - 1.3
     - 12:12:12:12:12:12 (arbitrary if directly connected)

|

**ICAP Service**

.. list-table::
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.50
   * - Services
     - ICAP Clamav
   * - Access
     - $ ``docker exec -it icap /bin/bash``

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Traffic Flow
     - BIG-IP Interface
     - Service IP Address
   * - In/Out
     - 1.2 (Tag 50)
     - 198.19.97.50
   * - REQ/RES URLs
     - /avscan
     - Port 1344

|

**Internal Web Server**

.. list-table::
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.80
   * - Services
     - Apache web server

       \*.f5labs.com
   * - Access
     - $ ``docker exec -it apache /bin/bash``

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Traffic Flow
     - BIG-IP Interface
     - Service IP Address
   * - In/Out
     - 1.2 (Tag 80)
     - 192.168.100.11 : Ports 80 & 443

       192.168.100.12 : Ports 80 & 443

       192.168.100.13 : Ports 80 & 443

|

**Juiceshop**

.. list-table::
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.80
   * - Services
     - NGINX app
   * - Access
     - $ ``docker exec -it nginx /bin/sh``

|

.. list-table::
   :header-rows: 1
   :widths: auto

   * - Traffic Flow
     - BIG-IP Interface
     - Service IP Address
   * - In/Out
     - 1.2 (Tag 80)
     - 192.168.100.20 : Ports 80 & 8443

|
.. warning::
   Simple passwords were used in this lab environment in order to make it easier for students to access the infrastructure. This does not follow recommended security practices of using strong passwords.

   This lab environment is only accessible via an authenticated student login.

