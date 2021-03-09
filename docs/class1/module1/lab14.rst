.. role:: red
.. role:: bred

Enable and Test Decrypted Behavior
==================================

Return to your SSL Orchestrator configuration browser tab on your local workstation. 
From the left-hand menu, navigate to :red:`SSL Orchestrator > Configuration`. 
Click on the :red:`sslo_L3_out` topology. In the list presented in black text, 
find the row labeled :red:`Security Policy`. Click on the pencil on the right. 
In the security policy, find the rule named :red:`All Traffic` and click on the pencil
on the right.  

-  **SSL Forward Proxy Action** - select the :red:`intercept` option.

Server certificate test
-----------------------

Return to your Ubuntu client RDP session.
Open a web browser (e.g., Firefox, Chromium) on the outbound client system and
navigate to any remote HTTPS site (e.g., https://www.google.com). Once the
site opens in the browser, check the server certificate of the site and verify
that it is now issued by the local CA configured in SSLO. This confirms that
the SSL forward proxy functionality enabled by SSL Orchestrator is now working correctly.

.. image:: ../images/module1-20.png
   :scale: 50 %
   :align: center

Decrypted traffic test on the security service
----------------------------------------------

Open a web browser (e.g., Firefox, Chromium) on the outbound client system and
navigate to https://eicar.org/?page_id=3950. Scroll down to the section labeled 
:red:`Download area using the secure, SSL enabled protocol HTTPS` and click on :red:`eicar.com`. 
This is a non-malicious file that antivirus products will detect for testing purposes. 
The decrypted malware test file is scanned by CLAM_AV.  This time, the download is prevented
and the user is presented a block page.

In the next section, you will test selective decryption based on URL category.