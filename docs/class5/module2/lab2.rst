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

The first interface is connected to the client-facing VLAN. The second interface is connected to the Internet-facing VLAN. The remaining interfaces are connected to various types of security services: L2, L3, HTTP, ICAP, and passive Tap. The SSL Orchestrator management interface is not shown.

.. image:: ./images/labinfo-1.png
   :align: left


Virtual Lab Infrastructure Details (and Credentials)
--------------------------------------------------------------------------------

The lab environment for this guide includes some prerequisite configuration settings that you
should be aware of. These are provided to simplify this course. If you wish to use
this lab guide with your own environment, please ensure that you create these objects in advance.

-  **Client side VLAN and subnet are pre-defined** - This is the VLAN
   that a client connects to for traffic flows. SSL Orchestrator does
   not define the client-side VLAN(s) and self-IP(s). A web server also
   exists to facilitate an inbound (reverse proxy) use case - external
   client to an internal set of websites.

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
   card numbers and other sensitive information could be exposed to
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
   services. While inspection services can be saves to CM and deployed later, they are generally
   deployed direct to an instance on creation, irrespective of applications, as they have network
   attributes that are typically specific to a BIG-IP Next instance. This will be made evident in
   the upcoming labs.


The following tables provide device/service network configuration details. Login credentials are also provided for use as directed in the lab exercises.


.. list-table:: **F5 BIG-IP Next Central Manager**
   :header-rows: 0
   :widths: auto

   * - Login
     - **Username**
     - **Password**
   * -
     - admin
     - Welcome123!
   * - **Interfaces**
     - **Self IP**
     - **Notes**
   * - *Management*
     - 10.1.1.6/24
     - Management
   * - System DNS
     - 10.1.1.1
     - 
   * - Gateway IP/DNS
     - 10.1.1.1
     - 


.. list-table:: **F5 BIG-IP Next SSL Orchestrator**
   :header-rows: 0
   :widths: auto

   * - **Credentials**
     - **Username**
     - **Password**
   * - *Admin User*
     - admin
     - Welcome123!
   * - **Interfaces**
     - **Self IP**
     - **Notes**
   * - *Management*
     - 10.1.1.7/24
     - Management VLAN
   * - *1.1*
     - 10.0.10.7/24
     - Client-Side VLAN (lab client)
   * - *1.2 (Tag 80)*
     - 192.168.100.7/24
     - Service-side (lab webservers)
   * - *1.2 (Tag 50)*
     - TBD
     - ICAP Service
   * - *1.2 (Tags 60 and 70)*
     - TBD
     - Inline L3 services
   * - *1.2 (Tags 30 and 40)*
     - TBD
     - Inline L3 services
   * - *1.3*
     - TBD
     - TAP service
   * - *1.4* / Future
     - TBD
     - Inline L2 service - Inbound
   * - *1.5* / Future
     - TBD
     - Inline L2 service - Outbound
   * - *1.6* / Future
     - TBD
     - Outbound Internet


.. list-table:: **Client (inbound/outbound)**
   :header-rows: 0
   :widths: 200 300 300

   * - **Interfaces**
     - **IP Address**
     - **VLAN**
   * - *eth1*
     - 10.1.10.50
     - Client-Side VLAN
   * - **Access**
     - **Username**
     - **Password**
   * - *SSH (UDF Web Console)*
     - N/A
     - N/A
   * - *Client Desktop (WebRDP)*
     - guacadmin
     - guacadmin
   * - *Admin Desktop (WebRDP)*
     - guacadmin
     - guacadmin


.. list-table:: **Ubuntu Server (Consolidated Services)**
   :header-rows: 0
   :widths: 200 300 300

   * - **Interfaces**
     - **IP Address**
     - **VLAN**
   * - *eth1*
     - 10.1.20.50
     - Inline L3 services
   * - *eth2*
     - 10.1.30.50
     - Tap service
   * - *eth3*
     - 10.1.40.50
     - Inline L2 service - Inbound
   * - *eth4*
     - 10.1.50.50
     - Inline L2 service - Outbound
   * - **Access**
     - **Username**
     - **Password**
   * - *SSH (UDF Web Console)*
     - N/A
     - N/A


.. list-table:: **Inline Layer 2 Service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host  -- ens8 and ens9

       br0 (bridge) tied to ens8 and ens9 interfaces on host
   * - Services
     - Suricata
   * - **Traffic Flow**
     - **BIG-IP Interface**
   * - Inbound
     - TBD
   * - Outbound
     - TBD


.. list-table:: **Inline Layer 3 Service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.60 and ens6.70
     - $ ``docker exec -it layer3 /bin/bash``
   * - Services
     - Firewall
     - 
   * - **Traffic Flow**
     - **BIG-IP Interface**
     - **Service IP Address**
   * - Inbound
     - 1.2 tag 60
     - 198.19.64.30/25
   * - Outbound
     - 1.2 tag 70
     - 198.19.64.130/25

.. list-table:: **HTTP Explicit Proxy Service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.30 and ens6.40
     - $ ``docker exec -it explicit-proxy /bin/bash``
   * - Services
     - Squid
     - Port 3128
   * - **Traffic Flow**
     - **BIG-IP Interface**
     - **Service IP Address**
   * - Inbound
     - 1.2 tag 30
     - 198.19.96.30/25
   * - Outbound
     - 1.2 tag 40
     - 198.19.96.130/25


.. list-table:: **TAP Service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens7
     - ens7 interface tied to tap service on host
   * - Services
     - Passive TAP
     - 
   * - **Traffic Flow**
     - **BIG-IP Interface**
     - **MAC Address**
   * - In/Out
     - 1.3
     - 12:12:12:12:12:12 (arbitrary if directly connected)


.. list-table:: **ICAP Service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.50
     - $ ``docker exec -it icap /bin/bash``
   * - Services
     - ICAP Clamav
     - 
   * - **Traffic Flow**
     - **BIG-IP Interface**
     - **Service IP Address**
   * - In/Out
     - 1.2 (Tag 50)
     - 198.19.97.50
   * - REQ/RES URLs
     - /avscan
     - Port 1344

.. list-table:: **Internal Web Server**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.80
     - $ ``docker exec -it apache /bin/bash``
   * - Services
     - Apache web server
     - \*.f5labs.com
   * - **Traffic Flow**
     - **BIG-IP Interface**
     - **Service IP Address**
   * - In/Out
     - 1.2 (Tag 80)
     - 192.168.100.11 : Ports 80 & 443

       192.168.100.12 : Ports 80 & 443

       192.168.100.13 : Ports 80 & 443


.. list-table:: **Juiceshop**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.80
     - $ ``docker exec -it nginx /bin/sh``
   * - Services
     - NGINX app
     - 
   * - **Traffic Flow**
     - **BIG-IP Interface**
     - **Service IP Address**
   * - In/Out
     - 1.2 (Tag 80)
     - 192.168.100.20 : Ports 80 & 8443


.. warning::
   Simple passwords were used in this lab environment in order to make it easier for students to access the infrastructure. This does not follow recommended security practices of using strong passwords.

   This lab environment is only accessible via an authenticated student login.

