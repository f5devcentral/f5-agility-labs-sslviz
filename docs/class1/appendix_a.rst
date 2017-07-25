Appendix - Common Testing Commands
==================================

The following are some simple, but powerful commands that are useful in
developing and troubleshooting SSL visibility projects.

**Controlling the SSLFWD certificate cache**

The behavior of the SSL Forward Proxy changes after a certificate is
cached, which will make it difficult to troubleshoot some issues. The
following allows you to both list and delete the certificates in the
cache.

``tmsh show ltm clientssl-proxy cached-certs clientssl-profile [CLIENTSSL PROFILE] virtual [INGRESS TCP VIP]``

``tmsh delete ltm clientssl-proxy cached-certs clientssl-profile [CLIENTSSL PROFILE] virtual [INGRESS TCP VIP]``

**Isolating SSLO traffic**

Any given website will be full of images, scripts, style sheets, and
very often references to document objects on other sites (like a CDN).
This can make troubleshooting very complex. The following cURL commands
allow you to isolate traffic to a single request and response.

``curl –vk https://www.bing.com``

``curl –vk --proxy 10.1.10.150:3128 https://www.bing.com/``

``curl –vk --proxy 10.1.10.150:3128 --location https://www.bing.com/``

Optionally, between each cURL test, delete the certificate cache and
start logging:

``tmsh delete ltm clientssl-proxy cached-certs clientssl-profile [CLIENTSSL PROFILE] virtual [INGRESS TCP VIP] && tail –f /var/log/ltm``

**Debugging**

There is simply nothing better than debug logging for troubleshooting
SSL intercept issues. The SSL Orchestrator in debug mode pumps out an
enormous set of logs, describing every step along a connection’s path.
Remember to never leave debug logging enabled.

``tail –f /var/log/ltm``

**Packet capture**

Second only to debug logging, packet captures are crucial to
troubleshooting any network-dependent issue.

``tcpdump –lnni [VLAN] [-Xs0]``

In-line services create "source" (S) and "destination" (D) VLANs, and
ICAP and receive-only services attach to existing VLANs. Drop a probe at
each point in the path and observe flow.

**SSL inspection**

``ssldump –AdNd –i [VLAN] port 443 <and additional filters>``

``tcpdump –i 0.0:nnn –nn –Xs0 –vv –w <file.pcap> <and additional filters>``

``ssldump –nr <file.pcap> -H –S crypto > text-file.txt``

TLS is rarely the issue, but a sight or configuration error may render
some sites inaccessible.

**Controlling the URL Filtering database**

To show the current status of the database:

``tmsh list sys url-db download-result``

To initiate (force) the URL DB to update:

``tmsh modify sys url-db download-schedule all status true download-now true``

To verify that the URL DB is actively updating:

``tcpdump -lnni 0.0 port 80 and host 204.15.67.80``

**External testing**

Plug the site’s address into SSLLabs.com server test site at
``https://www.ssllabs.com/ssltest/``
to see if the site has any unusual SSL/TLS requirements.
