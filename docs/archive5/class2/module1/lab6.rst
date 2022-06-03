.. role:: red
.. role:: bred

Test new Service Chain and Security Policy rules
================================================================================

-  Browse to ``https://www.example.com`` on your **Ubuntu18.04 Client** machine.

-  Verify that the web site is still being intercepted by confirming that the certificate is signed/verified by **f5labs.com** .

   |ff-f5labs-verified|

-  Verify that the Squid Proxy is seeing decrypted traffic:

   -  Return to the **Ubuntu18.04 Services** Web Shell (*Components > Ubuntu18.04 Services > ACCESS > Web Shell*)

   -  Enter the following commands in the Web Shell:

      .. code:: bash

         clear
         tail -f -n 0 /var/log/squid/access.log

   -  Visit a few secure (HTTPS) websites (non-banking) using Firefox on the **Ubuntu18.04 Client** machine and confirm that access is being logged. You should see log entries of the URLs visited.
   
   -  Visit a financial web site such as ``https://www.bankofamerica.com`` and verify that SSL Orchestrator is not intercepting TLS traffic. Confirm that the browser receives a server certificate that was issued by a trusted public CA. You should **not** see **Verified by: f5labs.com** because we are bypassing **Financial Data and Services** URLs in the SSL Orchestrator Security Policy.
   
   -  Check the Squid access log to confirm that the explicit proxy service is not seeing this bypassed (encrypted) traffic. Enter the following commands in the Web Shell:

      .. code:: bash

         clear
         tail -f -n 0 /var/log/squid/access.log

      .. note::
         You may still see log entries for analytics web sites that are associated with the financial web site.

   -  Press ``<CTRL+C>`` to stop the **tail** tool.


-  Verify that the Cisco Firepower TAP is seeing both intercepted and bypassed traffic:

   -  Return to the **Ubuntu18.04 Services** Web Shell (*Components > Ubuntu18.04 Services > ACCESS > Web Shell*)

   -  Type the following command to verify that traffic is being sent to the TAP service:

      .. code:: bash

         tcpdump -nnXi ens9 not arp and not icmp

   -  Visit a financial institution website that is bypassed and verify that a copy of the traffic is seen on the TAP device

   -  Since the traffic is not intercepted/decrypted you will not be able to see any intelligible output (ex. an HTTP GET request)

   -  Visit ``https://www.google.com/`` and you should see some recognizable text in the packet dump
   
   -  Press ``<CTRL+C>`` to stop the **tcpdump** tool

   -  As another test, enter the following command:

      .. code:: bash

         tcpdump -nnXi ens9 not arp and not icmp | grep -i "agility"

   -  Now, use Google to search for ``F5 Agility``. Since SSL Orchestrator is intercepting/decrypting this web site, you are able to see into the payload of this communication. The grep filter you applied should display output similar to the example below:

      |tcpdump-grep-agility|

   -  Press ``<CTRL+C>`` to stop the **tcpdump** tool

-  Close the web browser.


.. attention::
   This is the end of the lab module.


.. |ff-f5labs-verified| image:: ../images/ff-f5labs-verified.png
   :alt: Verified By: f5labs.com

.. |tcpdump-grep-agility| image:: ../images/tcpdump-grep-agility.png
   :alt: tcpdump of TAP service
