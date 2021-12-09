.. role:: red
.. role:: bred

Create the SSL Orchestrator deployment for Secure Web Gateway (SWG)
===========================================================================

We will now use the SSL Orchestrator Guided Configuration to configure
the Secure Web Gateway Service.
topology.

.. image:: ../images/gc-path.png
   :align: center

The following steps will walk through the **Guided Configuration (GC)** UI to build a
simple transparent forward proxy.


Initialization
------------------

From the left-hand menu, navigate to
:red:`SSL Orchestrator > Configuration`.

.. image:: ../images/module1-1.png
   :align: center


Configuration review and prerequisites
-------------------------------------------

Take a moment to review the topology options and workflow configuration steps
involved. Optionally satisfy any of the :red:`DNS, NTP and Route` prerequisites
from this page. Keep in mind, however, that aside from NTP, the SSLO GC will
provide an opportunity to define DNS and route settings later in the workflow.

The SSLO Topology type for this lab will be **L3 Outbound Transparent Proxy**


.. NOTE::
   DNS and NTP settings have already been defined in this lab.

.. image:: ../images/Layer3_Outbound_Topology.PNG
   :align: center

-  No other configurations are required on this page, click :red:`Next`.

Topology Properties
-----------------------

.. image:: ../images/gc-path-1.png
   :align: center

SSLO creates discrete configurations based
on the selected topology. For example, in previous versions of SSLO,
a transparent and explicit forward proxy might be defined together.
In SSLO 5.0 and above, these are configured separately. An explicit
forward proxy topology will ultimately create an explicit proxy
listener and its relying transparent proxy listener, but the
transparent listener will be bound only to the explicit proxy tunnel.
If a subsequent transparent forward proxy topology is configured, it
will not overlap the existing explicit proxy objects. The Topology
Properties page provides the following options:

The **Protocol** option presents four protocol types:

-  **TCP** - this option creates a single TCP wildcard interception
   rule for the L3 Inbound, L3 Outbound, and L3 Explicit Proxy
   topologies.

-  **UDP** - this option creates a single UDP wildcard interception
   rule for L3 Inbound and L3 Outbound topologies.

-  **Other** - this option creates a single any protocol wildcard
   interception rule for L3 Inbound and L3 Outbound topologies,
   typically used for non-TCP/UDP traffic flows.

-  **Any** - this option creates the TCP, UDP and non-TCP/UDP
   interception rules for outbound traffic flows.

The SSL Orchestrator **Topologies** option page presents six
topologies:

-  **L3 Explicit Proxy** - this is the traditional explicit forward
   proxy.

-  **L3 Outbound** - this is the traditional transparent forward
   proxy. An L3 outbound topology is effectively a "routed hop"
   configuration, where the SSLO topology listener becomes a routed
   path on the way to external (ie. Internet) resources.

-  **L3 Inbound** - this is a reverse proxy configuration. Like the
   L3 outbound, L3 inbound is typically a routed hop configuration
   for traffic directed inbound. It can also behave as a traditional
   load-balanced application.

-  **L2 Inbound** - the layer 2 topology options insert SSLO as a
   bump-in-the-wire in an existing routed path, where SSLO presents
   no IP addresses on its outer edges. The L2 Inbound topology
   provides a transparent path for inbound traffic flows.

-  **L2 Outbound** - the layer 2 topology options insert SSLO as a
   bump-in-the-wire in an existing routed path, where SSLO presents
   no IP addresses on its outer edges. The L2 Outbound topology
   provides a transparent path for outbound traffic flows.

   **IMPORTANT**

   It is important to distinguish SSLO's layer 2 topology from those
   of other traditional layer 2 SSL visibility vendors. Layer 2
   solutions such as the Blue Coat SSL visibility appliance (SSLVA)
   limit the types of devices that can be inserted into the
   inspection zone to layer 2 and below, and devices must be directly
   connected to the appliance. An SSLO layer 2 topology only exists at
   the outer edges. Inside the inspection zone, full-proxy routing is
   still happening, so layer 3 and HTTP services can still function
   normally.

-  **Existing Application** - this topology is designed to work with
   existing LTM applications. Whereas the L3 Inbound topology
   provides an inbound gateway function for SSLO, Existing
   Application works with LTM virtual servers that already perform
   their own SSL handling and client-server traffic management. The
   Existing Application workflow proceeds directly to service
   creation and security policy definition, then exits with an
   SSLO-type access policy and per-request policy that can easily be
   consumed by an LTM virtual server.


**For this lab:**

-  Click on the :red:`Next` button at the bottom of the page.

-  **Name**: Enter some name (ex. ":red:`sslo_SWGTest`").

-  **Protocol**: Select :red:`TCP` - this will create a TCP
   interception rule.

-  **IP Family**: Select :red:`IPv4`

-  **Topology**: Select :red:`L3 Outbound`

   .. image:: ../images/module1-3.png
      :align: center

The **Topology** settings have been configured.

-  Click :red:`Save & Next` to continue to the next stage.


SSL Configurations
----------------------

.. image:: ../images/gc-path-2.png
   :align: center

This page defines the specific SSL settings for the selected topology (in this
case a forward proxy) and controls both client-side and server-side SSL
options. If existing SSL settings are available (from a previous workflow), it
can be selected and re-used. Otherwise, the SSL Configurations page creates new
SSL settings for this workflow. The **[Advanced]** options below are
available when "Show Advanced Settings" is enabled (top right).

For this lab, :red:`Create a new SSL profile`.


Client-side SSL
~~~~~~~~~~~~~~~

-  **[Advanced] Processing Options** - SSLO 7.1 added TLS 1.3 support
   for outbound topologies, but does not enable it by default. In this lab,
   leave this setting as is.

-  **Cipher Type** - cipher type can be a Cipher Group or Cipher String.
   If the former, select a previously-defined cipher group (from Local
   Traffic - Ciphers - Groups). If the latter, enter a cipher string that
   appropriately represents the client-side TLS requirement. For this lab,
   leave the :red:`Cipher String` option selected. The default **Cipher**
   string of :red:`DEFAULT` is optimal for most environments.

-  **Certificate Key Chain** - the certificate key chain
   represents the certificate and private key used as the
   "template" for forged server certificates. While re-issuing
   server certificates on-the-fly is generally easy, private key
   creation tends to be a CPU-intensive operation. For that
   reason, the underlying SSL Forward Proxy engine forges server
   certificates from a single defined private key. This setting
   gives customers the opportunity to apply their own template
   private key, and optionally store that key in a FIPS-certified
   HSM for additional protection. The built-in "default"
   certificate and private key uses 2K RSA and is generated from
   scratch when the BIG-IP system is installed. The pre-defined
   :red:`default.crt` and :red:`default.key` can be left as is.

-  **CA Certificate Key Chain** - an SSL forward proxy must
   re-sign, or "forge" remote server certificate to local clients
   using a local certificate authority (CA) certificate, and local
   clients must trust this local CA. This setting defines the
   local CA certificate and private key used to perform the
   forging operation. Click the pencil icon to :red:`Edit`, then select
   :red:`subrsa.f5labs.com` for both Certificate and Key, and
   click :red:`Done`.

.. NOTE::
   SSL Settings minimally require RSA-based template and CA
   certificates but can also support Elliptic Curve (ECDSA)
   certificates. In this case, SSLO would forge an EC certificate
   to the client if the TLS handshake negotiated an ECDHE_ECDSA
   cipher. To enable EC forging support, add both an EC template
   certificate and key, and EC CA certificate and key.

-  **[Advanced] Bypass on Handshake Alert** - this setting allows
   the underlying SSL Forward Proxy process to bypass SSL
   decryption if an SSL handshake error is detected on the server
   side. It is recommended to leave this :red:`disabled`.

-  **[Advanced] Bypass on Client Certificate Failure** - this
   setting allows the underlying SSL Forward Proxy process to
   bypass SSL decryption if it detects a Certificate request
   message from the server, as in when a server requires mutual
   certificate authentication. It is recommended to leave this
   :red:`disabled`.

   .. NOTE::
      The above two Bypass options can create a security vulnerability. If
      a colluding client and server can force an SSL handshake error, or
      force client certificate authentication, they can effectively bypass
      SSL inspection. It is recommended that these settings be left
      disabled.

Server-side SSL
~~~~~~~~~~~~~~~

-  **[Advanced] Processing Options** - SSLO 7.1 added TLS 1.3 support
   for outbound topologies, but does not enable it by default. In this lab,
   leave this setting as is.

-  **Cipher Type** - cipher type can be a Cipher Group or Cipher
   String. If the former, select a previously-defined cipher group
   (from Local Traffic - Ciphers - Groups). If the latter, enter a
   cipher string that appropriately represents the server-side TLS
   requirement. For most environments, :red:`DEFAULT` is optimal.

-  **Trusted Certificate Authority** - browser vendors routinely
   update the CA certificate stores in their products to keep up with
   industry security trends, and to account for new and revoked CAs.
   In the SSL forward proxy use case, however, the SSL visibility
   product now performs all server-side certificate validation, in
   lieu of the client browser, and should therefore do its best to
   maintain the *same* industry security trends. BIG-IP ships with a CA
   certificate bundle that maintains a list of CA certificates common
   to the browser vendors. However, a more comprehensive bundle can
   be obtained from the F5 Downloads site. For this lab, select the
   built-in :red:`ca-bundle.crt`.

-  **[Advanced] Expire Certificate Response** - SSLO performs
   validation on remote server certificates and can control what
   happens if it receives an expired server certificate. The options
   are **drop**, which simply drops the traffic, and **ignore**,
   which mirrors an expired forged certificate to the client. The
   default and recommended behavior for forward proxy is to :red:`drop`
   traffic on an expired certificate.

-  **[Advanced] Untrusted Certificate Authority** - SSLO performs
   validation on remote server certificates and can control what
   happens if it receives an untrusted server certificate, based on
   the Trusted Certificate Authority bundle. The options are
   **drop**, which simply drops the traffic, and **ignore**, which
   allows the traffic and forges a good certificate to the client.
   The default and recommended behavior for forward proxy is to :red:`drop`
   traffic on an untrusted certificate.

-  **[Advanced] OCSP** - this setting selects an existing or can
   create a new OCSP profile for server-side Online Certificate
   Status Protocol (OCSP) and OCSP stapling. With this enabled, if a
   client issues a Status_Request message in its ClientHello message
   (an indication that it supports OCSP stapling), SSLO will issue a
   corresponding Status_Request message in its server-side TLS
   handshake. SSLO will then forge the returned OCSP stapling
   response back to the client. If the server does not respond with a
   staple but contains an Authority Info Access (AIA) field that
   points to an OCSP responder URL, SSLO will perform a separate OCSP
   request. The returned status is then mirrored in the stapled
   client-side TLS handshake.

-  **[Advanced] CRL** - this setting selects an existing or can
   create a new CRL profile for server-side Certificate Revocation
   List (CRL) validation. With this enabled, SSLO attempts to match
   server certificates to locally-cached CRLs.

The **SSL** settings have now been configured.

-  Click :red:`Save & Next` to continue to the next stage.


- **Authentication List**

   SSL Orchestrator now supports an option to include Authentication services such as
   an **Online Certificate Status Protocol (OCSP)**.  For this lab we will not be
   leveraging the **Authentication** option.   Click :red: `Save & Next`


.. image:: ../images/swg-authentication.PNG


Services List
-----------------
The Services List page is used to define security
services that attach to SSLO. For this lab we will use the SSLO Guided
Configuration to insert the F5 Secure Web Gateway (SWG) as an inline security
service in a service chain for decrypted traffic. This lab will create a
Transparent Layer-3 SWG service as well as pre-configured Per-Session
and a default Access Policy which can be modified once the deployment has been
completed.


  Click on the **F5** from the list of Service Properties and select
  **F5 Secure Web Gateway** then click on Add, and click on Save.


.. image:: ../images/swg-services-F5SWG.PNG
   :align: center


   Note the Access Profile and the Per Request Policy as follows
   (/Common/ssloS_F5_SWG.app/ssloS_F5_SWG_M_accessProfile and /common/SWGTest1)

   Enter **Default** for the **Named Scope**

   Select the /Common/SWGTest1 Per Request Policy then click on Save


.. image:: ../images/swg-services.PNG


Services Chain List
-----------------

  Click **Add** enter a name e.g. **SWGtestchain**
  Ensure the **ssloS_F5_SWG** is selected the click
  the right-arrow

  Click on save

  The ssloSC_swgservicetext should already by added as the only
  Service Chain element.


Security Policy
-------------------

.. image:: ../images/gc-path-5.png
   :align: center

   Security policies are the set of rules that govern how traffic is processed in
   SSLO. The "actions" a rule can take include:

- Whether or not to allow the traffic

- Whether or not to decrypt the traffic

- Which service chain (if any) to pass the traffic through

  Enter a name for the Security Policy, then click on Save & Next


Interception Rule
---------------------

.. image:: ../images/gc-path-6.png
   :align: center

Interception rules are based on the selected topology and define the "listeners"
that accept and process different types of traffic (ex. TCP, UDP, other). The
resulting LTM virtual servers will bind the SSL settings, VLANs, IPs, and
security policies created in the topology workflow.

The only configuration option in this lab is to
select the /Common/client-vlan within the **Ingress Network**
section and select the **right arrow**.  Click on **Save & Next**


.. image:: ../images/module1-12.png

The **Interception Rules** have now been configured.

**Your Security Policy should look similar to the image below**


.. image:: ../images/sslo_security_policy.PNG


.. image:: ../images/sslo_security_policy1.PNG
   :align: center


  **The Default Rule should be set to Intercept
  and the Service Chain should the SSLOSC_f5OnlyChain**



Egress Setting
------------------

.. image:: ../images/gc-path-7.png
   :align: center

Traffic egress settings are now defined per-topology and manage both the
default gateway route and outbound SNAT settings.

-  **Manage SNAT Settings** - enables per-topology instance SNAT settings. For
   this lab, select :red:`Auto Map`.

-  **Gateways** - enables per-topology instance gateway routing. The options
   include: use the system Default Route, use an existing gateway pool, or
   create a new gateway. For this lab, select :red:`Default Route`.

.. image:: ../images/module1-13.png

The **Egress Settings** have now been configured.

-  Click :red:`Save & Next` to continue to the next stage.


Log Settings
-----------------

.. image:: ../images/gc-path-8.png
   :align: center

Log settings are defined per-topology. In
environments where multiple topologies are deployed, this can help to
streamline troubleshooting by reducing debug logging to the affected
topology.

Multiple discreet logging options are available:

-  **Per-Request Policy** - provides log settings for security policy
   processing. In Debug mode, this log facility produces an enormous
   amount of traffic, so it is recommended to only set Debug mode for
   troubleshooting. Otherwise the most appropriate setting is :red:`Error`
   to log only error conditions.

-  **FTP** - specifically logs error conditions for the built-in FTP
   listener when FTP is selected among the additional protocols in
   the Interception Rule configuration. The most appropriate setting
   is :red:`Error` to log only error conditions.

-  **IMAP** - specifically logs error conditions for the built-in
   IMAP listener when IMAP is selected among the additional protocols
   in the Interception Rule configuration. The most appropriate
   setting is :red:`Error` to log only error conditions.

-  **POP3** - specifically logs error conditions for the built-in
   POP3 listener when POP3 is selected among the additional protocols
   in the Interception Rule configuration. The most appropriate
   setting is :red:`Error` to log only error conditions.

-  **SMTP** - specifically logs error conditions for the built-in
   SMTP listener when SMTP is selected among the additional protocols
   in the Interception Rule configuration. The most appropriate
   setting is :red:`Error` to log only error conditions.

-  **SSL Orchestrator Generic** - provides log settings for generic
   SSLO processing. If Per-Request Policy logging is set to Error,
   and SSL Orchestrator Generic is set to Information, only the SSLO
   packet summary will be logged. Otherwise the most appropriate
   setting is :red:`Error` to log only error conditions.


.. image:: ../images/module1-14.png

The **Log Settings** have now been configured.

-  Click :red:`Save & Next` to continue to the next stage.

Summary
------------

.. image:: ../images/gc-path-9.png
   :align: center

The summary page presents an expandable list of all of the workflow-configured
objects. To expand the details for any given setting, click the corresponding
arrow icon on the far right. To edit any given setting, click the corresponding
pencil icon. Clicking the pencil icon will send the workflow back to the
selected settings page.


.. image:: ../images/module1-15.png

- When satisfied with the defined settings, click :red:`Deploy`.

Upon successfully deploying the configuration, SSL Orchestrator will now
display a **Configure** view:

.. image:: ../images/swg-final-deployment.PNG


In the above list you will notice the following Virtual Servers have been created:

- The **ssloS_F5_SWG-t-4** listener.

- The **sslo_SWG-Test-in-t-4** listener.

- The **ssloS_F5_SWG-t-6** listener defines normal non-TCP/non-UDP IPv4 traffic.

This completes the configuration of SSL Orchestrator deployment
for Secure Web Gateway (SWG).
