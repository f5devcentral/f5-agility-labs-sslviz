F5 Networks

Agility 2020 Orlando

SSL-Orchestrator 201

Participant Hands-on Lab Guide

|image0|

    Last Updated: *1.2020*

    s.ghani@f5.com

©2016 F5 Networks, Inc. All rights reserved. F5, F5 Networks, and the F5
logo are trademarks of F5 Networks, Inc. in the U.S. and in certain
other countries. Other F5 trademarks are identified at f5.com.

Any other products, services, or company names referenced herein may be
trademarks of their respective owners with no endorsement or
affiliation, express or implied, claimed by F5.

These training materials and documentation are F5 Confidential
Information and are subject to the F5 Networks Reseller Agreement. You
may not share these training materials and documentation with any third
party without the express written permission of F5.

WHAT IS THE F5 SSL ORCHESTRATOR?
================================

F5 SSL Orchestrator (SSLO) provides an all-in-one appliance solution
designed specifically to optimize the SSL infrastructure, provide
security devices with visibility of SSL/TLS encrypted traffic, and
maximize efficient use of that existing security investment. This
solution supports policy-based management and steering of traffic flows
to existing security devices, designed to easily integrate into existing
architectures, and centralizes the SSL decrypt/encrypt function by
delivering the latest SSL encryption technologies across the entire
security infrastructure.

Multi-layered security
----------------------

In order to solve specific security challenges, security administrators
are accustomed to manually chaining together multiple point products,
creating a bare-bones “security stack” consisting of multiple services.
A typical stack may include components like Data Leak Prevention (DLP)
scanners, Web Application Firewalls (WAF), Intrusion Prevention and
Detection Systems (IPS and IDS), Malware Analysis tools, and more. In
this model, all user sessions are provided the same level of security,
as this “daisy chain” of services is hard-wired.

Dynamic service chaining
------------------------

Dynamic service chaining effectively breaks the daisy chain paradigm by
processing specific connections based on context provided by the
Security Policy, that then allows specific types of traffic to flow
through arbitrary chains of services. These service chains can include
five types of services: layer 2 inline services, layer 3 inline
services, receive-only services, ICAP services, and HTTP web proxy
services.

Topologies
----------

Different environments call for different network implementations. While
some can easily support SSL visibility at layer 3 (routed), others may
require these devices to be inserted at layer 2. SSL Orchestrator can
support all of these networking requirements with the following topology
options:

+-----+----------------------------------+---------+-----------------------------+
| •   |     Outbound transparent proxy   |     •   |     Inbound reverse proxy   |
+=====+==================================+=========+=============================+
| •   |     Outbound explicit proxy      |     •   |     Existing application    |
+-----+----------------------------------+---------+-----------------------------+
| •   |     Outbound layer 2             |     •   |     Inbound layer 2         |
+-----+----------------------------------+---------+-----------------------------+

Security Policy
---------------

The SSLO Security Policy provides a rich set of context-aware methods to
dynamically determine how best to optimize traffic flow through the
security stack. Context can minimally come from the following:

+-------------------------------------------+---------------------------------------------------------+------------------------+----------------------+
| • Source and destination address/subnet   |     •                                                   |     Destination port   |
+===========================================+=========================================================+========================+======================+
| •                                         |     URL filtering and IP intelligence - Subscriptions   |     •                  |     IP geolocation   |
+-------------------------------------------+---------------------------------------------------------+------------------------+----------------------+
| •                                         |     Host and domain name                                |     •                  |     Protocol         |
+-------------------------------------------+---------------------------------------------------------+------------------------+----------------------+

|image1|

    Topology System Settings SSL Configuration Service Service Chain
    Security Policy Interception Rule Summary

    **Users/Devices**

**SSL Orchestrator**

    Firewall Internet

    User

    Scalable services architecture

    Device-agnostic design

    Web Gateway DLP/ICAP IDS/TAP IPS/NGFW

WHAT’S NEW IN SSLO?
===================

SSLO 4.0 provides significant architectural improvements over previous
versions. Here are just a few of those updates:

-  SSLO 4.0 replaces the complex iRules-based traffic classification and
       service chaining functions of previous versions with an Access
       per-request policy engine, providing much greater flexibility in
       traffic management options.

-  SSLO 4.0 optimizes traffic flow through security services by
       replacing the complex “proxy hops” with a new “tee connector” –
       essentially a mid-proxy tap – that allows decrypted traffic to
       flow through security devices out-of-band from the main
       client-server proxy traffic. This is implemented as new “Service”
       and “Connector” profiles.

-  SSLO 4.0 introduces new “split session” client and server SSL
       profiles, that are now responsible for carrying SNI signaling
       information across the inspection zone.

-  SSLO 4.0 further optimizes traffic flow by reducing the amount of
       iRule data plane management, also making it easier to add
       customization iRules.

-  SSLO 4.0 introduces three new network topologies. Along with the
       existing outbound transparent and explicit proxy flows, 4.0 now
       also supports inbound layer 3 (reverse proxy) inspection, and
       layer 2 transparent inbound and outbound topologies.

SSLO 4.0 also includes the following new functionality features:

-  Explicit and transparent web proxy devices as an inline security
       service.

-  Front-end explicit proxy authentication via APM integration (relies
       on existing SWG-Explicit access policy).

-  FTPS (passive), SMTPS, POP3S, and IMAPS protocols inspection.

-  ICAP advanced filtering via LTM CPM policy (relies on an existing CPM
       policy).

-  URL filtering as a function of the Access per-request service
       chaining policy.

-  Authentication headers - ability to define additional HTTP headers to
       pass to inline security services.

-  vCMP support - ability to select existing VLANs for inbound and
       outbound to/from inline services.

SSLO 5.0 includes the following updates:

-  Guided Configuration user experience, a complete refresh of the SSLO
       UI based on the Access Guided Configuration engine.

-  Discreet “topology” definitions and the ability to define how SSLO
       listens for and processes traffic flows.

-  Re-entrant, wizard-driven workflows. Based on the selected topology,
       SSLO 5.0 presents an intuitive workflow UI that walks the user
       through a simplified object creation process.

|image2|

**Note**: Viprion chassis platform support is not available in SSLO 4.0
and 5.0.

SSLO 6.0 includes the following updates:

-  Transparent proxy captive portal authentication – In transparent
       forward proxy mode, an APM authentication profile
       (SWG-Transparent) can now be applied to perform captive
       portal-based client authentication.

-  Reverse proxy (inbound SSLO) TLS 1.3 support – TLS 1.3 can now be
       handled on both client and server side of SSLO for inbound SSLO
       topologies.

-  Service device monitor configuration – It is now possible to define
       the monitors applied to inline service definitions.

-  Improved analytics dashboard – SSLO now provides a separate analytics
       dashboard with enhanced statistical information.

-  Viprion chassis support – SSLO can now function on Viprion platforms,
       in both vCMP and non-vCMP configurations.

-  Improved stability over previous versions

WHAT’S NEW IN SSLO 7.1?
=======================

**SSL Orchestrator 7.1** adds the following new features:

-  **TLS 1.3 full proxy support for inbound and outbound flows** – SSLO
       6.0 included TLS 1.3 support for inbound (reverse proxy). This
       latest version now supports TLS 1.3 for outbound (forward proxy).
       A lab is dedicated to configuring TLS 1.3.

-  **Contextual security policies** – In previous versions SSLO made no
       distinction between inbound and outbound flows for security
       policies, allowing inconsistent rule options to break traffic.
       SSLO 7.1 now creates separate inbound and outbound security
       policy types.

-  **Access to full IP Intelligence categories** – This version provides
       access in the security policy to select specific IP Intelligence
       categories, versus simply ‘good’ or ‘bad’.

-  **Update fix to URL category lookup when URLDB/SWG not provisioned**
       – SSLO now correctly only queries custom URL categories if URLDB
       and/or SWG are not provisioned.

-  **Update fix to URL category lookup for custom categories** – SSLO
       now correctly queries the categories directly based on http://
       and https:// schemes. Previous versions only matched https://
       URLs.

-  **Update fix to inline service load balancing** – SSLO now correctly
       load balances inline services when port remapping is enabled.

-  **Strict Updates and modification enhancements** – In previous
       versions when strict-updates was disabled on a configuration
       object, that object would become read-only in the SSLO UI. In
       SSLO 7.1, for most object types, strictness can be disabled and
       still editable in the SSLO UI. If any non-strict changes are made
       to the objects, deployment provides an option to keep those
       non-strict changes or overwrite. A lab is dedicated to strict
       updates modification.

-  **New HA Status UI** – The HA Status UI provides a graphical view of
       HA state applicable to SSLO, including Gossip and Echo state. A
       lab is dedicated to configuring SSLO in HA mode.

-  **Several user interface, HA and upgrade stability enhancements** –
       This SSLO version is mainly targeted at stability improvements,
       including UI, HA and upgrades.

Please refer to the official SSLO 7.0 release notes for detailed update
information:

*https://techdocs.f5.com/kb/en-us/products/ssl-orchestrator/releasenotes/product/relnote-ssl-orchestrator-15-1-0-iapp-7-0.html*

Please refer to the official SSLO 7.1 release notes for details update
information:
*https://techdocs.f5.com/kb/en-us/products/ssl-orchestrator/releasenotes/product/relnote-ssl-orchestrator-15-1-0-iapp-7-1.html*

This lab guide and corresponding UDF lab environment are prepared for
SSLO 7.1 on a BIG-IP 15.1 instance.

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

-  **Required objects and Access policy for password-less authentication
       have been pre-created –** These objects are created using the APM
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

|image3|

**Note**: It is a security best practice to isolate security devices
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

+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     BIG-IP management IP   |     10.1.1.x (UDF-managed)                                       |                                  |              |                        |
+==================================+============================+==================================================================+==================================+==============+========================+========================+====+
|                                  |     Gateway IP/DNS         |     10.1.20.1                                                    |                                  |              |                        |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     Login                  |     admin:admin \| root:default                                  |                                  |              |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |     Client VLAN                  |              |     1.1                |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|     **SSL Orchestrator**         |                            |                                                                  |     Outbound VLAN                |              |     1.2                |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     Interfaces             |     ICAP service                                                 |                                  |     1.3      |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |     Inline L2 service inbound                                    |                                  |     1.4      |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |     Inline L2 service outbound   |     1.5      |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |     Inline L3/HTTP services      |              |     1.6 (tagged)       |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |     TAP service                  |              |     1.7                |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |                        |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|     **Inline layer 2 service**   |     Login                  |     student:agility                                              |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |                        |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|     **Inline layer 3 service**   |     Login                  |                                                                  |     student:agility              |              |                        |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     Interfaces             |                                                                  |     Inbound interface            |              | 1.6 tag 10             |     198.19.64.65/25    |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |     Outbound interface           |              | 1.6 tag 20             |     198.19.64.130/25   |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |                        |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     Login                  |     root:default                                                 |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|     **Explicit proxy service**   |     Interfaces             |     Inbound interface                                            |                                  | 1.6 tag 30   |     198.19.96.66/25    |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |     Outbound interface                                           |                                  | 1.6 tag 40   |     198.19.96.131/25   |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |                        |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     Services               |     Squid                                                        |                                  | Port 3128    |                        |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |     DansGuardian                                                 |                                  | Port 8080    |                        |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |                        |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|     **Receive-only service**     |     Login                  |     root:default                                                 |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     MAC address            |     12:12:12:12:12:12 (arbitrary if directly connected)          |                                  |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|     **ICAP service**             |     Login                  |     root:default                                                 |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     IP Address:port        |     10.1.30.50:1344                                              |                                  |              |                        |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     REQ/RES URLs           |     /squidclamav                                                 |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     Login                  |     root:default                                                 |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     IP Addresses           |     10.1.10.90                                                   |                                  |              |                        |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|     **Internal web server**      |                            |                                                                  |     10.1.10.91                   |              |                        |                        |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     \*.f5labs.com          |     10.1.10.92 (Apache2 instances listening on HTTPS port 443)   |                                  |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |     10.1.10.93                   |              |                        |                        |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |     10.1.10.94                   |              |                        |                        |    |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|     **Outbound client**          |     Login                  |     student:agility                                              |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     IP address             |     10.1.10.50 (RDP and SSH)                                     |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|     **Inbound client**           |     Login                  |     student:agility                                              |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |     IP address             |     10.1.20.55 (RDP and SSH)                                     |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+
|                                  |                            |                                                                  |                                  |              |                        |
+----------------------------------+----------------------------+------------------------------------------------------------------+----------------------------------+--------------+------------------------+------------------------+----+

+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|                                                                                                              |     AD server management IP   |     10.1.1.x (UDF-managed)         |                                       |                        |                        |
+==============================================================================================================+===============================+====================================+=======================================+========================+========================+====+
|                                                                                                              | Client VLAN address           |     10.1.10.200                    |                                       |                        |                        |    |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|                                                                                                              |     Login                     |     Various as shown below         |                                       |                        |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|                                                                                                              |                               |                                    |     AD Group/username                 |                        |     Password           |    |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|     **Active Direct Server and Client machine to test password-less authentication (Windows 2016 server)**   |                               |                                    |     Accounting/ac-user1, 2 & 3        |                        |     Same as username   |    |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|                                                                                                              |     Credentials               | Content-creators/cc-user1, 2 & 3   |                                       |     Same as username   |                        |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|                                                                                                              |                               |                                    |                                       |                        |                        |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|                                                                                                              |                               |     CSO-Office/cs-user1, 2 & 3     |                                       |     Same as username   |                        |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|                                                                                                              |                               |                                    |     HR/hr-user1, 2 & 3                |     Same as username   |                        |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|                                                                                                              |                               |                                    |     IT/it-user1, 2 & 3                |                        |     Same as username   |    |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+
|                                                                                                              |                               |                                    |     Security-Admins/sa-user1, 2 & 3   |                        |     Same as username   |    |
+--------------------------------------------------------------------------------------------------------------+-------------------------------+------------------------------------+---------------------------------------+------------------------+------------------------+----+

+----+----+----+----+----+----+----+----+
|    |    |    |    |    |    |    |    |
+====+====+====+====+====+====+====+====+
+----+----+----+----+----+----+----+----+

LAB 1 – Modify inspection services
==================================

The majority of enterprise forward proxy configurations will involve a
single or HA pair of F5 platforms performing the SSL visibility task.
The SSL Orchestrator has been designed with that principle in mind and
performs robust and dynamic service chaining of security devices. This
lab is designed to help leverage dynamic service chaining of security
devices.

Scenario:
---------

With the increase in the number of security incidents that have made the
news lately, your organization has updated its security policy to log
all user traffic flowing through the SSL Orchestrator irrespective of
whether the traffic has been inspected or bypassed. A new appropriately
sized Cisco Firepower L2 device has been purchased and has been cabled
to the SSL Orchestrator device. As the SSL Orchestrator Administrator,
your manager is needing you to do the following things:

1) In addition to the intercepted traffic being inspected by the Squid
   Proxy device, the traffic needs to be directed to the Cisco Firepower
   device

2) For traffic that was being bypassed, the still encrypted traffic
   needs to be directed to the Cisco Firepower device

Lab overview:
-------------

This lab assumes familiarity with SSL Orchestrator. The lab is
pre-staged with a deployment that is already configured with the
following Security Policy

|image4|

Please modify the above Security Policy to satisfy the requirements from
the Scenario described. Please following the step by step directions
that follow to successfully complete this task.

Step 0: Verify that the current solution works
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  **Validate that current SSLO deployment works**

   -  From the Lab deployment page, Select ***Components***. Screenshot
      shown below

|image5|

-  For the ***AD server & Testing Client*** system in the ***Systems***
   section of the interface click on ***Access->RDP***

-  Save the link for the RDP session and open the file

-  An RDP session to the AD server and Client should open using
   Microsoft RDP client

-  Login in as ***cs-user1/cs-user1*** for the domain ***f5labs***

-  Double-click on the FireFox icon on the desktop

-  Navigate to `*https://www.google.com* <https://www.google.com>`__

-  Click on the |image6| icon in the address bar

-  Click on the |image7|\ adjacent to the ***Connection Secure***

-  Verify the verification is done by ***Google Trust Services***.

|image8|

-  Modify proxy settings to traverse the SSLo setup

   -  Click on |image9|\ menu in FireFox to access FireFox settings

   -  Select ***Options*** and type in ***proxy*** in the Search box on
      the top right side of the FireFox window

   -  Select ***Settings*** for ***Configure how Firefox connects to the
      internet.*** menu option.

   -  Please modify the settings to reflect the screenshot below

|image10|

-  Click ***OK***

-  Close the ***Options*** tab and **close and re-open** the Firefox
   browser

-  Re-visit `*https://www.google.com* <https://www.google.com>`__

-  Verify that verification is done by ***f5labs.com*** now

|image11|

-  Visit a financial institution (*example*
   `*https://www.chase.com* <https://www.chase.com>`__) and verify that
   we are not intercepting traffic by ensuring that the verification is
   done by a trusted PKI issuer (*example JPMorgan Chase and
   Co./Entrust, Inc.*). If the traffic was intercepted we would see the
   that the verification would have been done by ***f5labs.com***. Since
   we are bypassing ***Financial Institutions*** and this website is a
   financial institution, the verification is done by the original
   issuer.

-  **Verify that the HTTP Proxy is seeing decrypted traffic**

-  From the lab deployment screen select ***Access->WEB SHELL*** from
   the ***Service - ExpProxy*** system

-  Type *tail -F /var/log/squid3/access.log* in the web console terminal

-  Visit a few secure(https) websites in the RDP client and verify that
   access is being logged even though we are visiting a secure website.
   You should see the log scrolling by and logging the sites and URLs
   visited. Your screen should have something similar to the screenshot
   shown below.

|image12|

Step 1: Review the current SSL Orchestrator deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Select ***SSL Orchestrator*** from the Main Menu and select
   ***Configuration*** from the submenu. The following existing
   deployment should be present. It will take a few seconds to render
   this page.

|image13|

-  Select ***Security Policies*** from the screen shown above. You
   should now be presented with following screen.

|image14|

Select the ***ssloP\_f5labs\_explicit*** security policy and you should
be able to see the security policy that is currently present as shown at
the start of this lab.

Step 2: Create a new service for the Cisco Firepower device
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Select ***SSL Orchestrator->Configuration*** from the main menu

-  Select ***Services*** from the menu on the displayed screen on the
   right. Notice that the already configured HTTP Type inspection
   service ***ssloS\_SQID*** is already present.

-  Press the ***Add*** button shown below the menu display line

-  Type \ *firepower* in the ***Search*** box below the ***Service
   Settings***

-  Select ***Cisco Firepower Threat Defense TAP*** and press the
   ***Add*** button and enter values as shown below

   -  **Name –** provide a unique name to this service (example
      *Cisco\_FP*).

   -  **Description –** provide a description as needed (example *Cisco
      Firepower Tap device*).

   -  **MAC Address –** for a tap service that is not directly connected
      to the F5, enter the device’s actual mac address. For a tap
      service that is directly connected to the F5, the Mac Address does
      not matter and can be arbitrarily defined. For this lab, enter
      *12:12:12:12:12:12.*

   -  **VLAN –** this defines the interface connecting the F5 to the TAP
      service. Click *Create New* and provide a unique name (example
      *TAP\_in*).

   -  **Interface –** select the *1.3* interface.

   -  **Tag –** this is the 802.1q VLAN tag for service. Leave it
      *empty* as we will be using an untagged interface.

   -  **Enable Port Remap –** this setting allows SSLO to remap thee
      port of HTTPS traffic flowing to this service. For this lab, leave
      the option *disabled (unchecked)*.

-  Click *Save & Next* button.

**Step 3: Create a new Service Chain with HTTP service and the Cisco Firepower service**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  You should not be in the Services Chain List menu

-  Click on ***Add.***

-  **Name –** provide a unique name for this service chain (example
   *all\_devices*)

-  **Description –** provide a description for this service chain
   (example *Squid Proxy and Cisco Firepower TAP*)

-  **Services –** Select both services from the ***Services Available***
   and move it to the ***Selected Service Chain Order*** section

-  Click ***Save***

Step 4: Create a new Service Chain for just the Cisco Firepower service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  You should be back at the ***Services Chain List*** interface again.

-  Click on ***Add.***

-  **Name –** provide a unique name for this service chain (example
   *Cisco\_TAP*)

-  **Description –** provide a description for this service chain
   (example *Cisco Firepower TAP only*)

-  **Services –** Select *ssloS\_Cisco\_FP* services from the
   ***Services Available*** and move it to the ***Selected Service Chain
   Order*** section

-  Click ***Save***

-  You should now have 3 items in the ***Services Chain List*** section

-  Click on ***Save & Next***

-  Click on ***Deploy***. This action will take a few seconds. Verify
   that the deployment was successful with no errors.

-  When successfully deployed, the screen should look like the
   following.

|image15|

Step 5: Modify the security policy to add the correct Service Chains
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  You should now be in the main ***Configuration*** section of the
   ***SSL Orchestrator*** main menu.

-  Select ***Security Policies*** from the list of options presented.

-  Select ***ssloP\_f5labs\_explicit*** from the list shown in the list.
   This should be the only selection on the list.

-  Click on the pencil icon next to the ***Pinners\_Rule*** |image16|

-  In the section shown below – click on menu selection for ***Service
   Chain->ssloSC\_Cisco\_TAP*** and press ***OK.***

|image17|

-  Repeat the same process for ***Finance\_Bypass***

-  Now select ***All Traffic*** and select ***ssloSC\_all\_devices***
   and press ***OK***.

-  The screen should now look like the picture shown below.

|image18|

-  Press ***Deploy*** and select ***Ok*** from the ***Continue Save?***
   pop up menu.

-  Click on ***Deploy***. This action will take a few seconds. Verify
   that the deployment was successful with no errors.

Step 6: Verify that everything is working as expected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Revisit the sites visited from ***Step 0:***

-  Re-visit `*https://www.google.com* <https://www.google.com>`__

-  Verify that verification is done by ***f5labs.com*** now

|image19|

-  Visit a financial institution (*example*
   `*https://www.chase.com* <https://www.chase.com>`__) and verify that
   we are not intercepting traffic by ensuring that the verification is
   done by a trusted PKI issuer (*example JPMorgan Chase and
   Co./Entrust, Inc.*). If the traffic was intercepted we would see the
   that the verification would have been done by ***f5labs.com***. Since
   we are bypassing ***Financial Institutions*** and this website is a
   financial institution, the verification is done by the original
   issuer.

-  **Verify that the HTTP Proxy is seeing decrypted traffic**

-  From the lab deployment screen select ***Access->WEB SHELL*** from
   the ***Service - ExpProxy*** system

-  Type *tail -F /var/log/squid3/access.log* in the web console terminal

-  Visit a few secure(https) websites in the RDP client and verify that
   access is being logged even though we are visiting a secure website.
   You should see the log scrolling by and logging the sites and URLs
   visited. Your screen should have something similar to the screenshot
   shown below.

|image20|

-  **Verify that the Cisco TAP is seeing both intercepted and bypassed
   traffic**

   -  From the lab deployment screen select ***Access->WEB SHELL*** from
      the ***Service – TAP*** system

   -  Type the following command to verify that the traffic is being
      sent to the tap device: *tcpdump -nnnni eth1 not arp and not icmp
      -X*

   -  Visit a financial website that is bypassed and verify that traffic
      is still flowing through the tap device

   -  Since the traffic is not de-crypted we will not be able to see any
      intelligible output

   -  Visit an intercepted website like https://www.google.com and we
      should see some recognizable text – to verify type the following
      commnd

      -  *tcpdump -nnnni eth1 not arp and not icmp -X \| egrep
         "Agility"*

   -  While still visiting the an encrypted website, since we are
      intercepting and decrypting it, we are able to see the payload and
      therefore the search above should return results when we search
      for “Agility 2020” in the browser.

   -  We should see something similar to the screenshot below

|image21|

LAB 2 – Working with Pinned certificate sites
=============================================

A few companies have chosen to enhance the protection of their SSL
websites by adding a process called as ***Pinning***. Pinning requires a
client that is controlled by the same company as well. When a
certificate is pinned, the native client will not accept a certificate
issued by any other entity. By intercepting traffic, we are issuing a
certificate on the fly that is issued by ***f5labs.com*** in this lab.
Since this certificate is not issued by the entity that is trusted by
the native client, the client will not allow further function. A great
example is Dropbox, with its Dropbox native client (not visiting the
website through the browser).

This lab is designed to demonstrate the impact of pinned certificates
with SSLo Orchestrator intercepting the traffic and how-to workaround to
make sure that these clients are enabled to work if required by company
policy.

Scenario:
---------

To prevent large attachments from clogging up the email system, your
company had enacted a new policy that restricts the size of email
attachments from the previously generous 10MB to 500K or less. When this
policy was enacted, employees were unable to send presentations or
office documents to each other. This prevented collaboration.

To fix this problem, your company signed up for Dropbox to facilitate
easy file transfers between employees. While this worked flawlessly
prior to deploying SSL Orchestrator, employees are no longer able to
access Dropbox using the native client after SSL Orchestrator has been
deployed. They are however able to visit Dropbox and do their operations
using a browser. However, the client provides certain functions that
cannot be replicated by the browser and the native client also provides
a richer and more convenient user experience.

You are tasked with fixing this such that both browser and native client
have unhindered access. Your manager has empowered you to do what is
necessary to get this working.

Lab overview:
-------------

This lab will continue work from the previous Lab 1. We will be
reviewing the Pinned certificates category and see how to modify it to
find a solution to the stated problem.

Step 0: Verify complaint
~~~~~~~~~~~~~~~~~~~~~~~~

-  On the Firefox browser in the ***AD server & Testing Client***, visit
   `*https://www.dropbox.com* <https://www.dropbox.com>`__

-  Verify that the SSL Orchestrator is intercepting it by checking the
   entity verifying the certificate

|image22|

-  Start the Dropbox client. The Dropbox client will be unable to
   connect to the server and show the following error. This error occurs
   because as we can see from the previous step, Dropbox.com is being
   intercepted by the SSL Orchestrator and client uses Certificate
   Pinning.

|image23|

-  To handle such issues, the default SSL Orchestrator Security Policy
   includes a rule called ***Pinners\_Rule*** that is the first rule in
   any Security Policy.

|image24|

Step 1: Review Pinned Certificate list
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  To review the list of URLs that compromise the ***Pinners***
   category, please review the list by selecting ***Access*** from the
   main menu and then ***Secure Web Gateway->URL Categories***. The
   following screen should be presented.

|image25|

-  Expand the ***Custom Categories*** (first item on the list) and
   select ***Pinners (custom)*** that will now appear. The URL list for
   Pinners should now be presented.

|image26|

-  Verify that Dropbox.com is not in the list presented in the
   ***Associated URLs*** list

Step 2: Add Dropbox to Pinned Certificate list
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  In the Pinners list ***Category Properties***

   -  Ensure that the ***Default Action*** dropdown menu has *Allow*
      selected

   -  Enter `*https://\*.dropbox.com/* <https://*.dropbox.com/>`__ in
      the ***URL*** text box. The trailing ***‘/’*** is important and
      cannot be omitted

   -  Verify that ***Glob Pattern Match*** checkbox is *Checked*

   -  Click on ***Add*** below the **Glob Pattern Match**

   -  Click on ***Update***

   -  Verify that ***https://\*.dropbox.com/*** is in the updated list
      of ***Associated URLs***

Step 3: Verify problem fixed with client and browser
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Perform the same steps from ***Step 0:***

   -  The browser will reflect that the traffic is not being intercepted
      and should show that the certificate is validated by the original
      entity.

|image27|

-  Restart the Dropbox client. The client should connect and the default
   browser will open requesting sign in. This indicates that the client
   has been able to establish a connection to the Dropbox server and is
   now requesting credentials to open a specific Dropbox.

N\ |image28|

-  ***Note:** When added to the Pinners list, the default action is that
   the SSL Orchestrator bypasses the traffic. In this lab example, since
   we have enabled a Layer 2 TAP device for all Intercepted as well
   Bypassed traffic, we still have some visibility. However, since the
   traffic is not de-crypted, the payload is still encrypted.*

**
**

LAB 3 – Transparent authentication using NTLM
=============================================

While SSL Orchestrator provides visibility into SSL traffic, the amount
of data that is logged is large. This prevents easy troubleshooting and
a mapping of traffic to originating person can be a difficulty process
especially if there are shared computers in the workplace.

To help with this and provide better manageability, SSL Orchestrator
provides the ability to enable transparent password-less authentication
using industry tested mechanisms like NTLM and Kerberos authentication.

This lab shows the process that is required enable NTLM authentication.
The authentication objects and Access Policy required for the completion
of this lab have already been completed and setup for you.

Scenario:
---------

Your manager lets you know that the company is looking to update its
Security Policy to log the usernames for all intercepted traffic. You
are tasked with developing a working Proof of Concept and are asked to
come up with an action plan to do so with the following restrictions:

1. This process needs to be transparent to the user that has already
   authenticated to the domain

Lab overview:
-------------

This lab will continue work from the previous Lab 2. We will configure
the SSL Orchestrator to authenticate using NTLM (the security objects
and the Access Policy) have already been configured to keep this lab
relevant only to the SSL Orchestrator.

Step 0: Verify that we are not authenticating users
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  From the main menu, select ***Access->Overview->Active Sessions***.
   The following screen should be presented.

|image29|

-  Browse through different websites on the ***AD server & Test
   Client*** browser.

-  Refresh the previously shown screen and notice that no sessions are
   being created.

-  Modify the ***Auto Refresh Setting*** to *30 seconds*

Step 1: Review the Security Objects and Access Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  From the main menu select ***Access->Authentication->NTLM->NTLM Auth
   Configuration*** and select *f5labs.com-NTLM-AAA* from the presented
   list (should be only one item in the list). The following screen
   should be presented.

|image30|

-  Machine Account Name is the name of the security object that is added
   to the domain as a Computer Account and Domain Controller FQDN List
   contains a list of the domain servers. In this lab environment we are
   using the Testing Client as the AD server as well.

-  From the main menu select ***Access->Profiles/Policies/Access
   Profiles (Per-Session Policies)***. The following screen will be
   presented.

   |image31|

-  Click on the ***Edit*** button next to the *f5labs-ntlm-ap* Access
   Profile Name. The following Access Policy should present itself.

|image32|

-  Close the newly opened tab

Step 2: Attach the security policy to the SSL Orchestrator configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Select ***SSL Orchestrator->Configuration*** from the main menu

-  Select ***Interception Rules.*** The following screen will then be
   presented.

|image33|

-  Select *sslo\_f5labs\_explicit-xp-4*

-  Select */Common/f5labs-ntlm-ap* from the ***Access Profile*** pull
   down menu

-  Press ***Deploy*** at the bottom of the screen

-  Select ***Services*** from the ***SSL Orchestrator->Configuration***
   screen

-  Select *ssloS\_SQID* from the ***Services*** list

-  Click on the |image34|\ icon to the right of |image35|\ menu
   selection

-  Scroll down and click on the ***Authentication Offload*** checkbox
   and have the checkbox *Checked*

-  Click on ***Save & Next***

-  Click ***OK*** in the ***Continue Save?*** popup.

-  Click on ***Save & Next*** on the next screen

-  Click on ***Deploy.*** This will take a few seconds. Please verify
   that the Deployment was completed successfully without errors.

Step 3: Modify DNS settings to configure the AD server as DNS server (Lab only)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*This step is required in this environment because of DHCP on the
management interface. The DNS settings are modified to default DHCP
settings periodically.*

*Usually the F5 devices IP addresses are managed manually and this step
is not required.*

-  From the main menu select ***System->Configuration->Device->DNS***
   and delete the **DNS Lookup Server List** and add the following IP
   address to the list *10.1.10.200.* The configuration screen should
   look like the one shown below after the edit. Click ***Update*** at
   the bottom of the screen.

|image36|

Step 4: Verify that user information is being identified on the F5 SSL Orchestrator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  From the main menu select ***Access->Overview->Active Sessions***

-  On the ***AD server and Testing Client*** open up the Firefox browser
   and navigate through to any website

-  Notice that the user is now being prompted for credentials in
   Firefox. This is because Firefox needs to be told on which sites to
   automatically provide NTLM credentials

   -  In the address bar of the Firefox browser type in *about:config*

   -  Type in *ntlm* in the search box on the top of the browser. Modify
      the *network.automatic-ntlm-auth.allow-non-fqdn* and
      *network.automatic-ntlm.trusted-uris* such that the screen looks
      like below

|image37|

-  In the ***AD server & Testing Client*** machine browser, browse
   through a few websites. You should now be able to browse without
   supplying credentials.

-  On the F5 device navigate to the ***Access->Overview->Active
   Sessions*** menu item from the main menu

-  You should be presented with session information and the username

|image38|

-  Click on *View* for the session – there is a lot of information that
   is displayed that is obtained from active directory. This confirms
   that the user has been authenticated and has been successfully looked
   up in Active Directory.

|image39|

.. |image0| image:: media/image1.jpeg
   :width: 1.93611in
   :height: 0.61667in
.. |image1| image:: media/image2.png
   :width: 5.52639in
   :height: 1.83542in
.. |image2| image:: media/image3.png
   :width: 7.20972in
   :height: 0.60347in
.. |image3| image:: media/image4.png
   :width: 7.20972in
   :height: 2.27986in
.. |image4| image:: media/image5.png
   :width: 7.05556in
   :height: 1.40417in
.. |image5| image:: media/image6.png
   :width: 7.05556in
   :height: 5.93264in
.. |image6| image:: media/image7.png
   :width: 0.23958in
   :height: 0.31250in
.. |image7| image:: media/image8.png
   :width: 0.42708in
   :height: 0.51042in
.. |image8| image:: media/image9.png
   :width: 4.67708in
   :height: 3.03125in
.. |image9| image:: media/image10.png
   :width: 0.41667in
   :height: 0.43750in
.. |image10| image:: media/image11.png
   :width: 7.05556in
   :height: 7.73125in
.. |image11| image:: media/image12.png
   :width: 4.57292in
   :height: 3.35417in
.. |image12| image:: media/image13.png
   :width: 7.05556in
   :height: 3.32778in
.. |image13| image:: media/image14.png
   :width: 7.05556in
   :height: 5.79861in
.. |image14| image:: media/image15.png
   :width: 6.85577in
   :height: 3.28888in
.. |image15| image:: media/image16.png
   :width: 7.05556in
   :height: 5.77361in
.. |image16| image:: media/image17.png
   :width: 0.22917in
   :height: 0.25000in
.. |image17| image:: media/image18.png
   :width: 4.45833in
   :height: 1.06250in
.. |image18| image:: media/image19.png
   :width: 7.05556in
   :height: 1.43681in
.. |image19| image:: media/image12.png
   :width: 4.57292in
   :height: 3.35417in
.. |image20| image:: media/image13.png
   :width: 7.05556in
   :height: 3.32778in
.. |image21| image:: media/image20.png
   :width: 7.05556in
   :height: 1.21944in
.. |image22| image:: media/image21.png
   :width: 7.05556in
   :height: 3.04444in
.. |image23| image:: media/image22.png
   :width: 4.63542in
   :height: 1.29167in
.. |image24| image:: media/image23.png
   :width: 7.05556in
   :height: 1.43264in
.. |image25| image:: media/image24.png
   :width: 7.05556in
   :height: 7.78333in
.. |image26| image:: media/image25.png
   :width: 7.05556in
   :height: 3.15486in
.. |image27| image:: media/image26.png
   :width: 7.05556in
   :height: 2.98958in
.. |image28| image:: media/image27.png
   :width: 7.05556in
   :height: 4.02986in
.. |image29| image:: media/image28.png
   :width: 7.05556in
   :height: 3.10764in
.. |image30| image:: media/image29.png
   :width: 6.87500in
   :height: 4.37500in
.. |image31| image:: media/image30.png
   :width: 7.05556in
   :height: 2.34097in
.. |image32| image:: media/image31.png
   :width: 6.37500in
   :height: 2.61458in
.. |image33| image:: media/image32.png
   :width: 7.05556in
   :height: 3.35694in
.. |image34| image:: media/image33.png
   :width: 0.26042in
   :height: 0.29167in
.. |image35| image:: media/image34.png
   :width: 1.86458in
   :height: 0.56250in
.. |image36| image:: media/image35.png
   :width: 7.05556in
   :height: 6.96528in
.. |image37| image:: media/image36.png
   :width: 7.05556in
   :height: 2.46111in
.. |image38| image:: media/image37.png
   :width: 7.05556in
   :height: 2.49722in
.. |image39| image:: media/image38.png
   :width: 7.05556in
   :height: 8.12986in
