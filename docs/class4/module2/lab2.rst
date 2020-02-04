.. role:: red
.. role:: bred

Step 2: Configure an L3 inbound SSLO deployment through Guided Configuration
----------------------------------------------------------------------------

In this scenario, an SSLO L3 inbound listener is configured either as a
gateway mode or application mode service. It will listen on a wildcard
VIP (0.0.0.0/0), or otherwise specific subnet (vs. a dedicated single
IP), and terminate inbound TLS traffic flows via wildcard or subject
alternative name (SAN) certificate. The :guilabel:`[Advanced]` options
below are available when :guilabel:`Show Advanced Settings` is enabled
(top right). Follow the :red:`L3 Inbound` topology workflow to build this
solution. In the SSL Orchestrator dashboard view, select the
:guilabel:`Topologies` tab (bottom) and click :guilabel:`Add`.

**Generic Settings**

- **Configuration review and prerequisites** - take a moment to review the
  topology options and workflow configuration, then click :guilabel:`Next`.

- **Topology Properties**

  - **Name**: provide some name (ex. ":red:`lab2_inbound`")

  - **Protocol**: :red:`TCP`

  - **IP Family**: :red:`IPv4`

  - **Topology**: select :red:`L3 Inbound`

  - Click :guilabel:`Save & Next`

- **SSL Configuration** - an inbound topology requires different SSL settings.

  - Click :guilabel:`Show Advanced Setting`

  - **Client-side SSL**

    - **[Advanced] Processing Options** - SSLO 7.1 provides TLS
      1.3 support for outbound topologies. For now, leave this as is.

    - **Cipher Type**: :red:`Cipher String`

    - **Cipher**: :red:`DEFAULT`

    - **Certificate Key Chain** - the certificate key chain represents the
      certificate and private key of an endpoint server instance (the target
      of a remote client's request). In a gateway-mode configuration, this
      would typically be a wildcard of Subject Alternative Name (SAN)
      certificate in the event the SSLO inbound listener was intended to
      service multiple sites. A wildcard certificate has been provided
      in this lab. Select the :guilabel:`pencil icon` to Edit, then select the
      :red:`wildcard.f5labs.com` certificate and private key and click
      :guilabel:`Done`.

      .. note:: SSL Settings minimally require RSA-based template and CA
         certificates but can also support Elliptic Curve (ECDSA) certificates.

  - **Server-side SSL**

    - **[Advanced] Processing Options** - SSLO 7.1 provides TLS
      1.3 support for outbound topologies. For now, leave this as is.

    - **Cipher Type**: :red:`Cipher String`

    - **Ciphera**: :red:`DEFAULT`

    - **Trusted Certificate Authority** - as an inbound solution, the
      server-side SSL would be pointing to internal servers. While it is
      possible to perform validation against internal server certificates, it
      is likely less important to do so. Leave this setting :red:`as is`.

    - **Expire Certificate Response** - Assuming no internal certificate
      validation is needed, the default **drop** setting will cause the
      connection to fail, so set this to :red:`Ignore`.

    - **Untrusted Certificate Authority** - Assuming no internal certificate
      validation is needed, the default **drop** setting will cause the
      connection to fail, so set this to :red:`Ignore`.

    - **[Advanced] OCSP** - Assuming no internal certificate validation is
      needed, any OCSP configuration will cause the connection to fail, so
      leave this :red:`as is`.

    - **[Advanced] CRL** - Assuming no internal certificate validation is
      needed, any CRL configuration will cause the connection to fail, so
      leave this :red:`as is`.

  - Click :guilabel:`Save & Next`.

- **Services List** - the same services can be leveraged here, so simply click
  :guilabel:`Save & Next`.

- **Service Chain List** - the same service chains can be leveraged here, so
  simply click :guilabel:`Save & Next`.

- **Security Policy** - the security policy requirements are specific
  to each organization, though an inbound security policy would likely
  be less complex than an outbound policy. Minimally assign a service
  chain to the existing **All Traffic** rule and click Save & Next.

  .. note:: SSL Orchestrator sends all traffic through an inline layer 3 or
     HTTP device in the same direction - entering through the service's
     "inbound" interface. It is likely, therefore, that the layer 3 device may
     not be able to correctly route both outbound (forward proxy) and inbound
     (reverse proxy) traffic at the same time. For more details, see:
     `Appendix - Routing considerations for layer 3 devices <../appendix/appendix3.html>`_


  - Remove the built-in :red:`"Pinners_Rule"` rule.
  - Edit the "All Traffic" policy to add the :red:`sub_service_chain` with the
    FireEye and TAP services (only), and click :guilabel:`OK`.
  - Click :guilabel:`Save & Next`

**Use case-specific settings**

- **Interception Rule** - here is where the gateway mode and
  application mode use cases are specifically defined. For this lab,
  select either the Gateway mode or Application mode below. It is also
  possible to perform this exercise twice, choosing a separate use case for
  each.

  1. **Gateway mode** - interception rule listening on a wildcard IP, port 443,
     with a wildcard or SAN certificate. Clients route through SSLO.

     - Click on :guilabel:`Hide Advanced Setting`

     - **Source Address**: :red:`0.0.0.0/0`

     - **Destination Address/Mask**: :red:`0.0.0.0/0`

     - **Port**: :red:`443`

     - **Security Policy Settings - Access Profile**: the Access
       Profile selection is exposed for inbound topologies to allow
       for insertion of per-session access and authentication
       processing. For this lab, leave this setting as :red:`default`.

     - **Ingress Network - VLANs**: select the :red:`outbound-vlan` (this is
       the server-side VLAN).

     - **L7 Profile Type** - this setting enables or disables HTTP
       processing.

     - **L7 Profile** - if the above option is set to HTTP, this
       option selects a specific HTTP profile. Set both to :red:`None`, or
       both to :red:`HTTP` and :red:`/Common/http`.


  2. **Application mode** - interception rule listening on a dedicated IP, port
     443, with any server certificate. Clients route to SSLO.

     - Click on :guilabel:`Show Advanced Setting`

     - **Source Address**: :red:`0.0.0.0/0`

     - **Destination Address/Mask**: :red:`10.1.20.120/32`

     - **Port**: :red:`443`

     - **Security Policy Settings - Access Profile**: the Access
       Profile selection is exposed for inbound topologies to allow
       for insertion of per-session access and authentication
       processing. For this lab, leave this setting as default.


     - **Ingress Network - VLANs**: :red:`outbound` (this is the
       server-side VLAN)

     - **Protocol Settings - Client TCP Profile**: allows setting a custom
       client-side TCP profile.

     - **Protocol Settings - Server TCP Profile**: allows setting a custom
       server-side TCP profile.

     - **Protocol Settings - SSL Configuration**: allows setting a custom SSL
       setting.

     - **Protocol Settings - L7 Profile Type**: this setting enables or
       disables HTTP processing.

     - **Protocol Settings - L7 Profile**: if the above option is set to
       HTTP, this option selects a specific HTTP profile.

     - **Pool** - :red:`webserver-pool` (pre-created server pool)

  - Click :guilabel:`Save & Next`

**Generic Settings**

- **Egress Settings** - traffic egress settings are now defined per-topology
  and manage both the gateway route and outbound SNAT settings.

  - **Manage SNAT Settings** - enables per-topology instance SNAT settings. For
    this lab, select :red:`Auto Map`.

  - **Gateways** - enables per-topology instance gateway routing. Options are
    to use the system default route, to use an existing gateway pool, or to
    create a new gateway. For this lab, select :red:`Default Route`.

  - Click :guilabel:`Save & Next`

- **Summary** - the summary page presents an expandable list of all of the
  workflow-configured objects. To expand the details for any given setting,
  click the corresponding arrow icon on the far right. To edit any given
  setting, click the corresponding :guilabel:`pencil icon`. Clicking
  the :guilabel:`pencil icon` will send the workflow back to the selected
  settings page.


- When satisfied with the defined settings, click :guilabel:`Deploy`.
