Appendix 1 - Common Testing Commands
====================================

The following are some simple, but powerful commands that are useful in
developing and troubleshooting SSL visibility projects.

**Packet capture**

Second only to debug logging, packet captures are crucial to troubleshooting
(and simply validating) network and service-related issues. Each security
service is connected to separate “ingress” and “egress” VLANs, traffic going
into the service from the F5, and traffic leaving the service back to the F5,
respectively. To verify that traffic is entering, or leaving a security device,
insert a tcpdump “tap” on the appropriate VLAN.

.. code-block:: bash
   
   tcpdump –lnni [VLAN]:nnn -Xs0

.. note:: The service VLANs reside with application service containers, so must
   be referenced accordingly. The easiest way to derive this path is from the
   BIG-IP UI. Navigate to the Network – VLANs menu. In the “Partition / Path”
   column for the desired VLAN, copy the path beyond the “Common/” string. For
   example, if the path is “Common/ssloN_IPS_in.app”, copy “ssloN_IPS_in.app”.
   The full path will be this value, plus the same string again without the
   “.app” extension. The VLAN path will therefore look like this:

   .. code-block:: bash

      ssloN_IPS_in.app/ssloN_IPS_in

From the BIG-IP command line, insert the tcpdump tap on the ingress side of
this IPS service like this:

.. code-block:: bash
   
   tcpdump -lnni ssloN_IPS_in.app/ssloN_IPS_in

Pass traffic through SSLO to verify that data is flowing to the inline service.
Switch the VLAN value to the egress VLAN to also verify data is flowing out of
the inline service. To view decrypted traffic, add “-Xs0” (zero) to the tcpdump
command.

.. code-block:: bash
   
   tcpdump -lnni ssloN_IPS_in.app/ssloN_IPS_in -Xs0

And to filter out ICMP traffic and other unneeded flows, add filters to the end
of the capture.

.. code-block:: bash
   
   tcpdump -lnni ssloN_IPS_in.app/ssloN_IPS_in not icmp

**Control the SSLFWD certificate cache**

The behavior of the SSL Forward Proxy changes after a certificate is cached,
which will make it difficult to troubleshoot some issues. The following allows
you to both list and delete the certificates in the cache.

.. code-block:: bash

   tmsh show ltm clientssl-proxy cached-certs clientssl-profile [CLIENTSSL PROFILE] virtual [INGRESS TCP VIP]

   tmsh delete ltm clientssl-proxy cached-certs clientssl-profile [CLIENTSSL PROFILE] virtual [INGRESS TCP VIP]

**Isolate SSLO traffic**

Any given website will be full of images, scripts, style sheets, and very often
references to document objects on other sites (like a CDN). This can make
troubleshooting very complex. The following cURL commands allow you to isolate
traffic to a single request and response.

.. code-block:: bash

   curl -vk https://www.bing.com

   curl -vk --proxy 10.30.0.150:3128 https://www.bing.com

   curl -vk --proxy 10.30.0.150:3128 --location https://www.bing.com

Optionally, between each cURL test, delete the certificate cache and start
logging:

.. code-block:: bash

   tmsh delete ltm clientssl-proxy cached-certs clientssl-profile [CLIENTSSL PROFILE] virtual [INGRESS TCP VIP] && tail –f /var/log/apm

**Debugging**

There is simply nothing better than debug logging for troubleshooting SSL
intercept issues. The SSL Orchestrator in debug mode pumps out an enormous set
of logs, describing every step along a connection's path. Remember to never
leave debug logging enabled.

.. code-block:: bash

   tail –f /var/log/apm

**SSL inspection**

.. code-block:: bash

   ssldump –AdNd –i [VLAN] port 443 <and additional filters>

   tcpdump –i 0.0:nnn –nn –Xs0 –vv –w <file.pcap> <and additional filters>

   ssldump –nr <file.pcap> -H –S crypto > text-file.txt

TLS is rarely the issue, but a sight or configuration error may render some
sites inaccessible.

**Control the URL Filtering database**

To show the current status of the database:

.. code-block:: bash

   tmsh list sys url-db download-result

To initiate (force) the URL DB to update:

.. code-block:: bash

   tmsh modify sys url-db download-schedule all status true download-now true

To verify that the URL DB is actively updating:

.. code-block:: bash

   tcpdump -lnni 0.0 port 80 and host 204.15.67.80*

**External testing**

Plug the site's address into SSLLabs.com server test site at
`https://www.ssllabs.com/ssltest/ <https://www.ssllabs.com/ssltest/>`__
to see if the site has any unusual SSL/TLS requirements.
