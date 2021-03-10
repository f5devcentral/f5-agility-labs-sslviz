.. role:: red
.. role:: bred

Pre-existing environment validation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Start an RDP session to the **Ubuntu18.04 Client** (*Components > Ubuntu18.04 Client > ACCESS > XRDP*)

.. image:: ../images/ubuntu-client-rdp-1.png

-  At the ubuntu Login prompt, click on the **OK** button to continue.

.. image:: ../images/ubuntu-client-rdp-2.png

|

.. tip::

   If the RDP session times out later, the password for the **student** user is ``agility``.


-  Open the **Firefox** browser

-  Browse to ``https://www.example.com/``

-  Click on the padlock icon in the address bar

   |ff-padlock|

-  Click the arrow to the right of **Connection secure**

   |ff-conn-expand|

-  Confirm that the connection/certificate is verified by **DigiCert Inc**

   |ff-digicert-verified|

-  Modify the client's proxy settings to point to F5 SSL Orchestrator

   -  In Firefox, click on the menu (|ff-menu|) in the top right of the window

   -  Select **Preferences** on the menu
   
   -  In the **Find in Preferences** search field at the top, type ``proxy``
   
   -  Click the **Settings...** button under Network Settings
   
   -  Select the **Manual proxy configuration** radio button. Ensure the proxy settings appear as follows:
   
      |ff-connection-settings|

-  Click the **OK** button

-  **Close and relaunch** the Firefox browser

-  Browse to ``https://www.example.com/`` once again

-  Confirm that the connection/certificate is now verified by **f5labs.com**

   |ff-f5labs-verified|

-  Confirm that the explicit proxy service is seeing decrypted traffic:

   -  Start a Web Shell to **Ubuntu18.04 Services** (**Components > Ubuntu18.04 Services > ACCESS > Web Shell**)

      .. image:: ../images/ubuntu-services.png

   -  Type the following command in the web console and hit Enter:

         ``docker exec -it explicit-proxy tail -f /var/log/squid/access.log`` 

   -  Visit a few secure (HTTPS) websites (non-banking) using Firefox on the **Ubuntu18.04 Client** machine and confirm that access is being logged even though we are visiting a secure website. You should see log entries of the sites and URLs visited, similar to the example below:

      |proxy-access-log|
      
   -  Visit a financial institution (ex. \https://www.bankofamerica.com) and verify that SSL Orchestrator is not intercepting by confirming that the verification is done by a trusted CA (ex. Entrust, Inc.). If the traffic was intercepted the connection/certificate would have been verified by **f5labs.com**. Because we are bypassing **Financial Institutions** in the SSL Orchestrator Security Policy and this website is a financial institution, the origin server's public certificate is presented to the client.

-  Confirm that the explicit proxy service is not seeing the bypassed (encrypted) traffic.


.. |ff-padlock| image:: ../images/ff-padlock.png
   :alt: Connection Padlock

.. |ff-conn-expand| image:: ../images/ff-conn-expand.png
   :alt: Site Information

.. |ff-f5labs-verified| image:: ../images/ff-f5labs-verified.png
   :alt: Verified By: f5labs.com

.. |ff-menu| image:: ../images/ff-menu.png
   :width: 14px
   :height: 14px
   :alt: Firefox Menu

.. |ff-digicert-verified| image:: ../images/ff-digicert-verified.png
   :alt: Verified By: DigiCert Inc

.. |ff-connection-settings| image:: ../images/ff-connection-settings.png
   :alt: Firefox Connection Settings

.. |proxy-access-log| image:: ../images/proxy-access-log.png
   :alt: Proxy Access Log
