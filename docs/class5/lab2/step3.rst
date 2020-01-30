Step 3: Verify problem fixed with client and browser
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Perform the same steps from **Step 0:**

   -  The browser will reflect that the traffic is not being intercepted
      and should show that the certificate is validated by the original
      entity.

   |image27|

-  Restart the Dropbox client. The client should connect and the default
   browser will open requesting sign in. This indicates that the client
   has been able to establish a connection to the Dropbox server and is
   now requesting credentials to open a specific Dropbox.

   |image28|

-  .. note:: **Note:** When added to the Pinners list, the default action is that
   the SSL Orchestrator bypasses the traffic. In this lab example, since
   we have enabled a Layer 2 TAP device for all Intercepted as well
   Bypassed traffic, we still have some visibility. However, since the
   traffic is not de-crypted, the payload is still encrypted.

.. |image27| image:: ../media/image026.png
   :width: 7.05556in
   :height: 2.98958in
.. |image28| image:: ../media/image027.png
   :width: 7.05556in
   :height: 4.02986in
