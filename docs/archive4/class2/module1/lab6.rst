.. role:: red

Confirm Service Chain and Security Policy rules are working as expected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Browse to ``https://www.example.com`` on your Windows 10 Desktop

-  Verify that :red:`https://www.example.com` is still being intercepted by confirming the certificate is signed/verified by **f5labs.com** 

   |ff-f5labs-verified|

-  Verify that the Squid Proxy is seeing decrypted traffic:

   -  Start a Web Shell to **Service - ExpProxy** (Components > Service - ExpProxy > ACCESS > Web Shell)

   -  Type ``tail -f /var/log/squid3/access.log`` in the web console and hit Enter

   -  Visit a few secure (HTTPS) websites (non-banking) using Firefox on the Windows 10 Desktop and confirm that access is being logged. You should see log entries of the URLs visited.
   
   -  Visit a financial institution (ex. \https://www.chase.com) and verify that SSL Orchestrator is not intercepting by confirming that the verification is done by a trusted CA (ex. Entrust, Inc.). If the traffic was intercepted the connection/certificate would have been verified by f5labs.com. Because you are bypassing **Financial Institutions** in the SSL Orchestrator Security Policy and this website is a financial institution, the origin server's public certificate is presented to the client.
   
   -  Confirm that the explicit proxy service is not seeing this bypassed (encrypted) traffic

-  Verify that the Cisco Firepower TAP is seeing both intercepted and bypassed traffic:

   -  Start a Web Shell to **Service - TAP** (Components > Service - TAP > ACCESS > Web Shell)

   -  Type the following command to verify that traffic is being sent to the TAP service:

         ``tcpdump -nnXi eth1 not arp and not icmp``

   -  Visit a financial institution website that is bypassed and verify that a copy of the traffic is seen on the TAP device

   -  Since the traffic is not intercepted/decrypted you will not be able to see any intelligible output (ex. an HTTP GET request)

   -  Visit ``https://www.google.com/`` and you should see some recognizable text in the packet dump
   
      -  To verify, type the following command:

            ``tcpdump -nnXi eth1 not arp and not icmp | egrep -i "agility"``

   -  Since SSL Orchestrator is intercepting/decrypting \https://www.google.com, you are able to see into the payload of this communication and therefore the grep filter you applied should display output when you search for ``Agility 2020`` in the browser, similar to the example below:

      |tcpdump-grep-agility|

.. |ff-f5labs-verified| image:: ../images/ff-f5labs-verified.png
   :width: 467px
   :height: 304px
   :alt: Verified By: f5labs.com
.. |tcpdump-grep-agility| image:: ../images/tcpdump-grep-agility.png
   :width: 728px
   :height: 128px
   :alt: tcpdump of TAP service
