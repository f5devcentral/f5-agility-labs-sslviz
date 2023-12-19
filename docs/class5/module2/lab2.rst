.. role:: red
.. role:: bred

Lab Environment Details
================================================================================


Network Diagram
--------------------------------------------------------------------------------

Here is a visual representation of the virtual lab environment. The numbers inside the right edge of the SSL Orchestrator box indicate the port numbers and VLAN tags (if applicable). The colored boxes to the right of the services respresent some product examples for each respective service type.

The first interface is connected to the client-facing VLAN. The second interface is connected to the Internet-facing VLAN. The remaining interfaces are connected to various types of security services: L2, L3, HTTP, ICAP, and passive Tap. The SSL Orchestrator management interface is not shown.

.. image:: ./images/labinfo-1.png
   :align: left


Virtual Lab Infrastructure Details (and Credentials)
--------------------------------------------------------------------------------

The lab environment for this guide has provided some prerequisite
settings that you should be aware of. These are provided to make the
demo simpler. All of the following would need to be configured manually
in another environment.

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

-  **CA certificate and private key are installed** - This is the CA
   certificate and private key that are used to re-issue (forge) remote
   server certificates to internal clients for outbound traffic flows.

-  **Server certificate and private key are installed** - For the
   inbound (reverse proxy) traffic flow use case, SSL traffic is
   terminated at the F5, and re-encrypted on the way to the internal
   application environment. A wildcard server certificate is installed
   to facilitate using any name under the “.\ *f5labs.com*\ ”
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
   devices exist in a “private enclave” local to the BIG-IP Next
   instance(s). Please keep this in mind when defining the network
   settings for the inspection services.*



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
     - **VLAN**
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
     - **VLAN**
   * - *Management*
     - 10.1.1.7/24
     - Management
   * - *1.1*
     - 10.1.10.7/24
     - Client-Side
   * - *1.2*
     - 10.1.20.7/24
     - Inline L3 services
   * - *1.3*
     - 10.1.30.7/24
     - Tap service
   * - *1.4*
     - 10.1.40.7/24
     - Inline L2 service - Inbound
   * - *1.5*
     - 10.1.50.7/24
     - Inline L2 service - Outbound


.. list-table:: **Ubuntu Client**
   :header-rows: 0
   :widths: 200 300 300

   * - **Interfaces**
     - **IP Address**
     - **VLAN**
   * - *eth1*
     - 10.1.10.50
     - Client-Side VLAN
   * - **Credentials**
     - **Username**
     - **Password**
   * - *Local Admin*
     - user
     - user
   * - *Guacamole User (web RDP)*
     - user
     - user


.. list-table:: **Ubuntu Server**
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
   * - **Credentials**
     - **Username**
     - **Password**
   * - *Local Admin*
     - ???
     - ???
   * - *Guacamole Admin*
     - guacadmin
     - guacadmin


.. list-table:: **Inline layer 2 service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host

       br0 (bridge) tied to ens8 and ens9 interfaces on host
   * - Services
     - Suricata
   * - **Traffic Flow**
     - **Interface**
   * - Inbound
     - ???
   * - Outbound
     - ???


.. list-table:: **Inline layer 3 service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.60 and ens6.70
     - $ ``docker exec -it layer3 /bin/bash``
   * - Services
     - ???
     - 
   * - **Traffic Flow**
     - **Interface**
     - **IP Address**
   * - Inbound
     - 1.2 tag 60
     - 198.19.64.30/25
   * - Outbound
     - 1.2 tag 70
     - 198.19.64.130/25

.. list-table:: **HTTP Explicit proxy service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.30 and ens6.40
     - $ ``docker exec -it explicit-proxy /bin/bash``
   * - Services
     - Squid
     - Port 3128
   * - **Traffic Flow**
     - **Interface**
     - **IP Address**
   * - Inbound
     - 1.2 tag 30
     - 198.19.96.30/25
   * - Outbound
     - 1.2 tag 40
     - 198.19.96.130/25


.. list-table:: **Tap service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens7
     - ens7 interface tied to tap service on host
   * - Services
     - ???
     - 
   * - **Traffic Flow**
     - **Interface**
     - **MAC Address**
   * - In/Out
     - ???
     - 12:12:12:12:12:12 (arbitrary if directly connected)


.. list-table:: **ICAP service**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.50
     - $ ``docker exec -it icap /bin/bash``
   * - Services
     - ICAP Clamav
     - 
   * - **Traffic Flow**
     - **Interface**
     - **IP Address**
   * - In/Out
     - ???
     - 198.19.97.50
   * - REQ/RES URLs
     - /avscan
     - Port 1344

.. list-table:: **Internal web server**
   :header-rows: 0
   :widths: auto

   * - Description
     - Ubuntu server host -- ens6.80
     - $ ``docker exec -it apache /bin/bash``
   * - Services
     - Apache web server
     - \*.f5labs.com
   * - **Traffic Flow**
     - **Interface**
     - **IP Address**
   * - In/Out
     - ???
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
     - **Interface**
     - **IP Address**
   * - In/Out
     - ???
     - 192.168.100.20 : Ports 80 & 8443


.. warning::
   Simple passwords were used in this lab environment in order to make it easier for students to access the infrastructure. This does not follow recommended security practices of using strong passwords.

   This lab environment is only accessible via an authenticated student login.

