.. role:: red
.. role:: bred

Enable Decryption and Test Behavior
===================================

This test will demonstrate that:

- Traffic is now being decrypted

- The "malicious" file will be detected and blocked by the network-based scanner.

Enable decryption within the security policy
---------------------------------------------------

- Return to SSL Orchestrator Guided Configuration.  

- Click on the :red:`sslo_L3_out` topology.

- In the configuration summary, find the row labeled :red:`Security Policy` and click on the pencil at the far right.

- In the security policy, find the rule  :red:`All Traffic` and click on the pencil at the far right.   

-  **SSL Forward Proxy Action** - select the :red:`Intercept` option.

- Click :red:`OK`.

- Click :red:`Save & Next`.

- Pause for a few seconds and the yellow banner shown below will appear at the very top of the :red:`Interception Rule` settings.

.. image:: ../images/reentrantdeploy.png
   :scale: 50 %
   :align: center

- Click :red:`Deploy`.

.. image:: ../images/deploysuccessful.png

- Click :red:`OK`.

Server certificate test
-----------------------

- Return to your Ubuntu client RDP session.

- Open a web browser (e.g., Firefox, Chromium) on the outbound client system and :red:`open a new incognito or private browsing session`. This is to ensure the browser establishes an entirely new session and does not reuse cached content.

- Once the site opens in the browser, check the server certificate of the site and verify that it is now issued by the local CA configured in SSLO. This confirms that the SSL forward proxy and certificate re-write functionality enabled by SSL Orchestrator is now working correctly.

.. image:: ../images/module1-20.png
   :scale: 50 %
   :align: center

**This confirms that the certificate re-write and SSL forward proxy decryption functionality provided by SSL Orchestrator has been enabled.**

Decrypted traffic test on the security service
----------------------------------------------

- Open a web browser (e.g., Firefox, Chromium) on the outbound client system and :red:`open a new incognito or private browsing session`. This is to ensure the browser establishes an entirely new session and does not reuse cached content.

- Navigate once again to https://eicar.org/?page_id=3950. Scroll down to the section labeled :red:`Download area using the secure, SSL enabled protocol HTTPS` and click on :red:`eicar.com`. 

.. image:: ../images/virus.png
   :scale: 50 %
   :align: center

**Notice that this time, the download is prevented and the user is presented a block page because the file was decrypted prior to scanning.**

In the next section, you will test selective decryption based on URL category.