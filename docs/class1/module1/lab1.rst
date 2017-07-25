Lab 1: Create a 1-box transparent Proxy SSLO
=============================================

The majority of enterprise configurations will involve a single F5
platform performing the SSL visibility task. The SSL Orchestrator has
been designed with that principle in mind and performs robust security
service chaining of security devices attached to a single appliance.
Extending SSLO to a two-box configuration simply creates an additional
decrypted “clear text” inspection zone between the two devices where a
limited set of non-service-chained security devices can be inserted. SSL
Orchestrator 2.0 now makes configuration of a single-box deployment
quite simple and intuitive. Please follow the steps below to create a
1-box transparent proxy SSL Orchestrator configuration.

Step 1: Review the lab diagram and map out the services and endpoints
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Review the lab diagram at the beginning of this document, and make note
of the security devices and interfaces assigned to those security
devices. The SSL Orchestrator iApp assumes that this information is
known so in your environment it’s important to first scope out and
define all of the pieces before starting assembly.

#. The client is attached to a ``10.20.0.0/24`` network and is assigned
   the IP ``10.20.0.60``. This network is attached to the BIG-IP 1.1
   interface.

#. The **L2 device** is an Ubuntu 14.04 LTS server configured to bridge
   its eth1 and eth2 interfaces. Its inbound VLAN (traffic to it) is
   attached to the BIG-IP ``1.7`` interface. Its outbound interface
   (traffic coming from it) is attached to the BIG-IP ``1.8`` interface.
   The box is running open source Suricata as a passive IPS.

#. The **L3 device** is an Ubuntu 14.04 LTS server configured to route
   from its eth1 to its eth2 interface. Its inbound VLAN (traffic to it)
   is attached to the BIG-IP ``1.4 (VLAN tag 50)`` interface and has an IP
   of ``198.19.1.64/25``. Its outbound interface (traffic coming from it)
   is attached to the BIG-IP ``1.4 (VLAN tag 60)`` interface and has an IP
   of ``198.19.1.130/25``. Its default gateway is ``198.19.1.245``, which
   will be a VLAN self-IP on the BIG-IP. The box is running open source
   Suricata as a passive IPS.

#. The **TAP** device is an Ubuntu 14.04 LTS server configured with a
   single eth1 interface. That interface is attached to the BIG-IP ``1.5``
   interface. The box is running open source Suricata as a passive IDS.

#. The **DLP/ICAP** device is an Ubuntu 14.04 LTS server configured with
   a single eth1 interface. That interface is attached to the BIG-IP
   ``1.6`` interface and has an IP of ``10.70.0.10``. The box is running
   c-icap and Squid/Clamav.

#. The outbound network is attached to the BIG-IP ``1.2`` interface, in
   the ``10.30.0.0/24`` subnet, and has a gateway of ``10.30.0.1``.

#. In the lab, client inbound, Internet outbound, and isolated TAP and
   DLP VLANs and self-IPs are already created. The (ADC) SSL
   Orchestrator iApp does not create these.

   |image1|

Step 2: Fulfill the SSL Orchestrator pre-requisites
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are a number of objects that the (ADC) SSL Orchestrator iApp does
not create, and expects to exist before deploying the iApp. You must
create the following objects before starting the iApp:

#. **Import the CA certificate and private key** – in order to terminate
   and re-encrypt outbound SSL traffic, SSL Forward Proxy must re-issue,
   or rather “forge” a new server certificate to the client. In order to
   perform this re-issuance process, the BIG-IP must possess a
   certificate authority (CA) certificate and associated private key.
   
   .. NOTE:: This lab environment already has a subordinate CA certificate and
      private key installed.

#. **Create the client inbound VLAN and self-IP** – create the VLAN and
   self-IP that connects the client to the BIG-IP. In this lab that’s
   the ``10.20.0.0/24`` subnet and interface ``1.1`` on the BIG-IP. This lab
   environment already has this VLAN and self-IP created.

#. **Create the Internet outbound VLAN and self-IP** – create the VLAN
   and self-IP that connects the BIG-IP to the outbound Internet router.
   In this lab that’s the ``10.30.0.0/24`` subnet and interface ``1.2`` on
   the BIG-IP. *This lab environment already has this VLAN and self-IP
   created*.

#. **Create the DLP VLAN and self-IP** – if it is desired to isolate the
   DLP/ICAP device, create the VLAN and self-IP that connects the DLP
   device to the BIG-IP. In this lab that’s the ``10.70.0.0/24`` subnet
   and interface ``1.6`` on the BIG-IP. The DLP security device is
   listening on ``10.70.0.10`` and ICAP is listening on port ``1344``. *This
   lab environment already has this VLAN and self-IP created*.

#. **Create the Receive Only VLAN and self-IP** – if it is desired to
   isolate the TAP device, create the VLAN and self-IP that connects the
   TAP device to the BIG-IP, In this lab that’s the ``10.50.0.0/24``
   subnet and interface ``1.5`` on the BIG-IP. The TAP device doesn’t
   specifically have an IP address on this subnet, but BIG-IP constructs
   access to passive devices with clone pools, which equates to an
   arbitrary IP address in a pool and static ARP entry from that IP
   address to the MAC address of the passive device. In other words,
   BIG-IP needs a VLAN in this arbitrary subnet, ``10.50.0.0/24``, a pool
   that points to an arbitrary unused IP address, ``10.50.0.5``, and a
   static ARP that points this IP address at the MAC address of the
   passive device. *This lab environment already has this VLAN and
   self-IP created*.

#. **Create the default internet route for outbound traffic** – the iApp
   provides an option to leverage a defined gateway pool, or use the
   system default route. If a gateway pool is not used, they system
   route table will need to have a default route used to reach Internet
   destination. *We’ll use a gateway pool defined within SSLO*.

#. **Create a log publisher** – this step is optional if you desire to
   push debug messages to an external Syslog server. There is no Syslog
   server in this lab environment, so you can skip this step.

Step 3: Configure the SSL Orchestrator General Properties section
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

|image2|

General Properties include all of the inbound and outbound networking,
and certificate signing options for the SSL Orchestrator configuration.
Please use the following settings for this lab:

#. **Application Service Name** – enter an arbitrary name for this SSLO
   configuration. This name cannot contain spaces or dashes.

#. **Do you want to setup separate ingress and egress devices with a
   cleartext zone between them?** – this question indicates if this is a
   single or two-box SSLO solution. Select ``No, use one BIG-IP device
   for ingress and egress`` to enable a single-box deployment.

#. **Which IP address families do you want to implement?** – SSLO can
   support IPv4 and IPv6 environments. In this environment, however,
   we’ll only be using IPv4. Select ``Support IPv4 only``.

#. **Which proxy schemes do you want to implement?** – SSLO supports
   transparent and explicit proxy schemes. In this first lab we’ll be
   setting up a transparent proxy, so select 
   ``Implement transparent proxy only``. A transparent proxy is fundamentally 
   a proxy service that the client is not generally aware of; and there 
   are a number of facilities by which to get client traffic to a 
   transparent proxy. The easiest option, and the one used in this lab, 
   is to make the proxy (SSLO ingress) the default outbound route for 
   the client. Other options include policy-based routing (PBR) and Web Cache
   Communication Protocol (WCCP), two techniques often employed by
   gateway devices to more intelligently steer traffic through
   potentially multiple outbound paths.

#. **Do you want to pass UDP traffic through the transparent proxy
   unexamined?** – if enabled, SSLO can also process UDP traffic
   separate, specifically to be able to block specific UDP traffic, or
   detect and block Google QUIC traffic. For this lab, select 
   ``Yes, Pass all UDP traffic unexamined``. You may also optionally select
   ``No, manage UDP traffic by classification``, whereby you’ll be
   presented with a separate UDP traffic classifier section on the
   Policies tab.

#. **Do you want to pass non-TCP, non-UDP traffic through the
   transparent proxy unexamined?** – SSLO will by default create a
   second non-TCP VIP to catch all non-TCP traffic, allowing the option
   to either allow that traffic or block it. If the above UDP traffic
   option is enabled, there would be three ingress VIPs, one for TCP,
   one for UDP, and one for everything else. In this lab, select
   ``Yes, pass Non TCP, Non UDP traffic``.

#. **Which is the SSL Forward Proxy CA certificate?** – assuming that a
   CA certificate has already been installed, select this certificate
   from the list. In this lab that will be the
   ``subca1.f5demolabs.com.crt`` certificate.

#. **Which is the SSL Forward Proxy CA private key?** – assuming that a
   CA private key has already been installed, select this private key
   from the list. In this lab that will be
   ``subca1.f5demolabs.com.key``.

#. **What is the private-key passphrase (if any)?** – if the CA private
   key requires a passphrase to unlock signing functions, enter that
   passphrase here. In this lab the subordinate CA private key does not
   require a passphrase.

#. **Which CA bundle is used to validate remote server certificates?** –
   this option is at the heart of SSL Forward Proxy, next to the
   selection of the CA certificate and private key. As a function of SSL
   Forward Proxy, SSLO must not only re-issue server certificates, but
   also validate the real server certificates. That validation involves
   both expiration and public key infrastructure (PKI) trust
   establishment. That trust establishment is made possible by the
   inclusion of a CA certificate trust store that allows the BIG-IP to
   build a complete trust chain form the real server certificate to an
   explicitly trusted set of locally-installed CA roots. Those CA
   certificates are stored in a bundle file and that bundle is
   represented in this configuration option. Without this CA bundle file
   SSLO cannot perform the PKI trust validation. The default
   ``ca-bundle.crt`` file is a bundle that is maintained and sourced
   from the Mozilla foundation, but larger more complete bundles are
   also available on the F5 Downloads site.

#. **Should connections to servers with expired certificates be
   allowed?** – if the real server certificate is expired, SSLO provides
   the option to either drop the connection, or to ignore the expired
   certificate and allow the connection to proceed. As of BIG-IP version
   12.0 and up, and expired certificate will generate an expired
   re-issued certificate to the client.

#. **Should connections to servers with untrusted certificates be
   allowed?** – if the real server certificate cannot be trusted, by way
   of the previously-detailed PKI trust process, SSLO provides the
   option to either drop the connection, or to ignore the untrusted
   certificate and allow the connection to proceed. Unlike an expired
   certificate, as of BIG-IP version 13.0, an untrusted certificate is
   still re-issued as a locally trusted certificate to the client.

#. **Should strict updates be enforced for this application?** – this is
   a standard iApp option that allows for, or denies write access to
   iApp-created objects (outside of the iApp).

#. **Which VLAN(s) will bring client traffic to the transparent proxy?**
   – this is the VLAN that client traffic will arrive at the BIG-IP.
   SSLO can process traffic from multiple incoming sources. In this lab
   that is ``client-vlan``.

#. **How should a server TLS handshake failure be handled?** – SSLO
   provides an option to bypass SSL inspection if the remote server
   issues an Alert during its SSL handshake. The default option is to
   deny the connection. The alternative ‘auto-bypass’ option is marked
   (INSECURE) because it has the potential of allowing a third party to
   bypass the SSL inspection process if they can control the behavior of
   the server.

#. **DNS query resolution** – in a transparent proxy configuration, DNS
   would only be used with the Dynamic Domain Bypass (DDB) traffic
   classification process, whereby a bypass decision is possible using
   the client’s ClientHello message Server name Indication (SNI) value.
   Alone this classifier would allow someone to bypass SSL inspection by
   simply creating a spoofed local Hosts entry for a site that is known
   to bypass SSL inspection. DDB prevents this spoofing by following the
   SNI check with a DNS query that replaces the destination address in
   the client’s packet with the value returned form DNS.

#. **Do you want to configure local/private DNS zones?** – this again is
   only used for DDB in a transparent proxy configuration.

#. **Do you want to use DNSSEC to validate DNS information?** – SSLO
   provides an option to use DNSSEC instead of raw DNS for that DDB
   spoofing prevention process.

#. **Do you want to SNAT client IP addresses?** – this option declares
   how traffic must egress from the SSLO solution. In this lab outbound
   SNAT is required, so select ``Yes, SNAT (replace) client addresses``.

#. **Do you want to use a SNAT Pool?** – with the above option enabled,
   this option allows you to use a defined SNAT pool or the built-in
   SNAT Auto-Map. Select ``No, Use SNAT Auto Map (not recommended)``.

#. **Should traffic go to the Internet via specific gateways?** – SSLO
   provides an option to use a system-defined gateway, or to create a
   load balanced pool of gateway addresses. Select 
   ``Yes, Send outbound / Internet traffic via specific gateways``.

#. **What are the IPv4 outbound gateway addresses?** – enter a ratio of
   ``1``, and ``10.30.0.1`` as the one outbound gateway address.

#. **What SSL Intercept logging level do you want to enable?** – SSLO
   provides three separate logging levels, based on verbosity. For this
   lab select, ``Debug. Log debug data as well as normal level
   data``. In a real world scenario, you would either *NEVER* enable
   debug logging on a production system, or create a log publisher and
   push those debug messages to an external Syslog.

#. **Which Log Publisher will process the log message?** – if you’ve
   created a log publisher, select it here. There is, however, no
   external Syslog service available in this lab.

#. **What kind of statistics do you want to record?** – an enormous
   amount of statistics can be generated by SSLO, both for external
   analysis via Splunk, or by the built-in SSLO Analytics engine powered
   by AVR.

Step 4: Add a Receive Only security service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

|image3|

A Receive Only device is one in which traffic does not pass **through**
it, but that a **copy** of the traffic flows to it. The most common type
of receive only, or “passive”, or “tap” device is an Intrusion Detection
System (IDS), but other security devices can also be passive. For
example, Symantec has a DLP product that runs as a passive device. In
this lab, an Ubuntu 14.0 LTS server is equipped with a single eth1
interface with no IP address, and that interface connects to the BIG-IP
on interface ``1.5``. The lab is also already configured with the VLAN and
self-IP of ``10.50.0.100/24``. Follow these steps to create a receive only
security device:

#. On the Receive Only Services tab of the SSL Orchestrator
   configuration, click the **Add** button.

#. Give the receive only service a name, example ``ids1``.

#. In the **Mac Address** field, enter the layer 2 address of the
   passive device, which in this case will be ``2c:c2:60:6e:cf:a2``.

#. In the **IP Address** field, enter an arbitrary IP address in the
   pre-established passive device VLAN self-IP subnet, which in this
   case could be ``10.50.0.5``.

#. In the **VLAN** list, select the associated */Common/tap-vlan* VLAN.

#. In the **Interface** list, select the associated interface, which in
   this case is ``1.5``.

#. Click the **Finished** button.

Step 5: Add an ICAP security services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

|image4|

An ICAP device is a security product that performs Data Loss Prevention
(DLP) functions, and possibly malware detection by way of the ICAP
protocol. ICAP functions by essentially “wrapping” a payload (usually
HTTP) with ICAP request and header information, and then sending that to
an ICAP service. The ICAP service can again perform many services,
including DLP and malware detection, and summarily either return the
payload untouched, modify the data (remove the sensitive information
and/or malware payload), or block and sever the connection. This can
apply to both request (client-to-server) and response (server-to-client)
payloads. In this lab an Ubuntu 14.04 LTS server is equipped with the
open source c-icap service and Squid and Clamav services to both
facilitate access to c-icap and provide virus/malware detection. Follow
these steps to create an ICAP security service:

#. On the ICAP Services tab of the SSL Orchestrator configuration, click
   the ``Add`` button.

#. Give the ICAP service a name, example ``icap1``.

#. In the ``ICAP Devices`` section, provide the IP address and listening
   port for the ICAP service, which in this case is ``10.70.0.10``, port
   ``1344``. Click the ``Add`` button to the right.

#. While not required for this lab, you have the option in the
   ``Headers`` list to insert custom headers on the way to the ICAP
   service.

#. In the ``TCP Connections`` list, select the desired connection
   behavior.

#. In the ``Request`` and ``Response`` field, enter the ICAP service’s
   specific URL. This will be different for every ICAP product (example:
   McAfee often uses the ``/REQMOD`` and ``/RESPMOD`` URLs). In this lab we’ll
   use the same Squid/Clamav service URL for request and response:

   ``icap://${SERVER\_IP}:${SERVER\_PORT}/squidclamav``

   The ``${SERVER_IP}`` and ``${SERVER_PORT}`` strings represent a variable
   substitution function to allow ICAP to be load balanced across a
   defined set of ICAP services.

#. In the ``Preview Max. Length (bytes)`` field, enter a byte value.
   This is the amount of data that needs to be sent to the ICAP service,
   and of course the larger this number the more latency the service
   incurs. In this lab Squid/Clamav requires a preview size of
   ``1048576``.

#. In the ``Server Failure Handling`` list, select the desired
   behavior if the ICAP service becomes unavailable.

#. On the ``Send HTTP/1.0 Requests to ICAP`` list, select whether to
   send both HTTP/1.1 and HTTP/1.0 requests (Yes), or only HTTP/1.1
   requests (No). Squid/Clamav will function with either selection.

#. Click the ``Finished`` button.

Step 6: Add inline security services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

|image5|

An inline device is one in which traffic flows through it, generally
with separate inbound and outbound interfaces. The current SSLO does not
support one-armed devices, so any inline security device must include
either separate interfaces, or a single multi-tagged interface.

#. **What is the IPv4 (CIDR/19) subnet block base address?** – the
   current SSLO platforms restrict layer 3 inline devices to a set of
   RFC2544 /25 (mask 255.255.255.128) in the 198.19.x.0 address space.
   This option provides some minimal capabilities to change that, but
   consider this. While it may seem counterintuitive to make this
   restriction, consider that prior to any SSL visibility solution, most
   enterprises 1) already have security devices in the network, and 2)
   those devices are plugged into existing networks along with other
   devices. When an SSL visibility solution is introduced into that
   environment, devices that previously only saw encrypted traffic are
   now being fed unencrypted payloads. If that devices remains plugged
   into existing environments with other devices, there is a high
   probability that some of those devices will be able to see that
   unencrypted traffic as well. In other words, it is a security best
   practice to now isolate security devices within an SSL visibility
   solution. All access into and out of that device, including
   management access, should be controlled by that SSL visibility
   product. To that end, it should make no difference what the IP
   addresses are on that security device, so changing them to suit the
   iApp’s requirements should not pose a significant challenge. In this
   lab, the one inline layer 3 device has an inbound eth1 interface
   listening on ``198.19.1.64/25``, an outbound interface listening on
   ``198.19.1.130/25``, and a default gateway of ``198.19.1.245``, which
   will be a BIG-IP self-IP on the destination VLAN side of that inline
   layer 3 device.

#. **Create an inline layer 2 security service (simulated FireEye)** –
   follow these steps to create the inline layer 2 security device
   definition:

   -  On the Inline Services tab of the SSL Orchestrator configuration,
      click the ``Add`` button.

   -  Give the inline layer 2 security service a name, example:
      ``FireEye``.

   -  Select ``Layer 2`` from the ``Service Type`` list.

   -  In the ``Interfaces`` area, select the inbound interface first
      (traffic going to the security device), which in this case is
      ``1.7``. Next select the outbound interface (traffic coming back to
      the BIG-IP), which in this case in ``1.8``. Whether VLAN tags are
      needed or not, enter tag values in the inbound and outbound tag
      field and then click the ``Add`` button to the right.

   -  From the ``Translate Port for HTTP Traffic`` list, select a
      translation port. This will be the port, as required, that
      decrypted (HTTP) traffic will be translated to as it passes
      through the security device. This setting is completely optional,
      but for demonstration, select ``Yes to Port 8080``.

   -  From the ``Connection Handling on Outage`` list, select the action
      you desire in the event that the layer 3 security device becomes
      unavailable.

   -  Click the ``Finished`` button.

#. **Create an inline layer 3 security service (simulated Palo Alto
   NGFW)** – follow these steps to create the inline layer 3 security
   device definition:

   -  On the Inline Services tab of the SSL Orchestrator configuration,
      click the ``Add`` button.

   -  Give the inline layer 3 security service a name, example:
      ``NGFW``.

   -  Select ``Layer 3`` from the ``Service Type`` list.

   -  In the ``Interfaces`` area, select the inbound interface first
      (traffic going to the security device), which in this case is 
      ``1.4 (VLAN tag 50)``. Next select the outbound interface (traffic coming
      back to the BIG-IP), which in this case is ``1.4 (VLAN tag 60)``.

   -  In the ``Available Devices`` area, select ``198.19.1.64`` (the
      inbound interface of the lab layer 3 device), and then click the
      **Add** button to the right.

   -  From the ``Translate Port for HTTP Traffic`` list, select a
      translation port. This will be the port, as required, that
      decrypted (HTTP) traffic will be translated to as it passes
      through the security device. This setting is completely optional,
      but for demonstration, select ``Yes to Port 8443``.

   -  From the ``Connection Handling on Outage`` list, select the action
      you desire in the event that the layer 3 security device becomes
      unavailable.

   -  Click the ``Finished`` button.

      .. NOTE:: The 3\ :sup:`rd` octet in the in-line layer 3 service IP range
         is defined by the order in which the in-line device was created. For
         example, if the first device created was a layer 3 device, it’s IP
         subnet would be *198.19.\ **0**.x/25*. If the first device was layer 2,
         and the second layer 3, the IP subnet for the layer 3 device would be
         *198.19.\ **1**.x/25*. A third device would be in the
         *198.19.\ **2**.x/25* subnet, etc. The in-line layer 3 security device
         in this lab uses the *198.19.1.x/25* subnet range, so it must be the
         *second* in-line device created in the SSLO configuration.

Step 7: Save and deploy the configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this lab you’ll just be defining the services without creating any
specific service chains or classifiers. All of the defined services
automatically populate a built-in ‘All’ chain, and the default action is
to send decrypted traffic through this chain if there are not specific
traffic classifier matches (which there won’t be yet). Click the
**Save** button in the upper right, and then click the **Deploy**
button. This should return a green button and a message that indicates
the deployment was a success. If that doesn’t happen, analyze the error
and re-review the steps outlined in this lab. If all else fails, skip
directly to Lab 3 and use the tools listed there to troubleshoot this
configuration.

Step 8: Test
~~~~~~~~~~~~

Assuming the deployment was successful, open a browser on the lab
Windows client and test accessing remote sites. You should see
unfettered access to Internet sites, and HTTPS sites with locally
re-issued server certificate.

|image6|

The Windows 7 box in the lab also has Cygwin installed, so you can test
from cURL using the following command line syntax:

``curl -vk https://www.bing.com``

In this lab, you also configured the ICAP service, which is running
Clamav and can detect certain types of Malware. To test this, navigate
to ``http://www.eicar.org/85-0-Download.html``, and attempt to download the
``eicar.com`` file under the http and https protocol sections (bottom of
the page). Clamav should catch this malware and present a blocking page
to the browser.

.. |image1| image:: /_static/class1/image1.png

.. |image2| image:: /_static/class1/image2.png
   :width: 7.05000in
   :height: 0.34167in
.. |image3| image:: /_static/class1/image3.png
   :width: 7.05000in
   :height: 0.36806in
.. |image4| image:: /_static/class1/image4.png
   :width: 7.05000in
   :height: 0.36736in
.. |image5| image:: /_static/class1/image5.png
   :width: 7.05000in
   :height: 0.35347in
.. |image6| image:: /_static/class1/image6.png
   :width: 2.48334in
   :height: 3.07886in
