.. role:: red
.. role:: bred

Testing the deployment
==============================

To test the deployed solution, RDP to the :bred:`Desktop-Outbound` client
machine.

.. hint:: Username = :red:`student` / Password = :red:`agility`

Server certificate test
-----------------------

Open a browser on the outbound system and navigate to any remote HTTPS site,
for example, https://www.google.com. Once the site opens in the browser,
check the server certificate of the site and verify that it has been issued
by the local CA configured in SSLO. This confirms that the SSL forward proxy
functionality enabled by SSL Orchestrator is working correctly.

.. image:: ../images/module1-11.png
   :scale: 75 %
   :align: center


Decrypted traffic analysis on the security services
---------------------------------------------------

Depending on the type of security service, it may be easier to log into the
console shell and run a similar tcpdump capture on the inbound or outbound
interface. A tcpdump capture usually requires root or sudo access.

Let's check if we see data on the TAP device.

-  In the UDF UI, select the **Access** drop down selection on the **Service - TAP** VM,
   then select **WEB SHELL**.

-  In the Shell window, use the following command for tcpdump. :red:`10.1.10.50` is
   the IP address of the client machine.

.. code-block:: bash

   sudo tcpdump -lnni eth1 -Xs0 host 10.1.10.50

-  Browse to an SSL site from the RDP hosts browser (ex: https://www.cnn.com)
   and notice that the TAP device is receiving traffic unencrypted.

-  Press CTRL+C to stop the tcpdump.

Let's check another security device. Perform a tcpdump on the IPS device to
observe the decrypted clear text traffic.

-  In the UDF UI, select the **Access** drop down selection on the
   **Service - Inline L3** VM, then select **WEB SHELL**.

-  In the shell window use the below command for tcpdump. 10.1.10.50 is the client
   machine and since we are doing port remap, the unecrypted traffic will arrive
   on port 8181.

.. code-block:: bash

   sudo tcpdump -lnni eth1.10 -Xs0 host 10.1.10.50 and port 8181

-  Browse to an SSL site from the RDP hosts browser (ex: https://www.cnn.com)
   and notice that the IPS device is receiving traffic unencrypted.

-  Press CTRL+C to stop the tcpdump.

-  Close out (exit) all Webshell windows.

.. attention:: This is the end of the lab module.
