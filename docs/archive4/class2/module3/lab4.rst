.. role:: red

Enable authentication offload
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Start a Web Shell to **Service - ExpProxy** *(Components > Service - ExpProxy > ACCESS > Web Shell)*

-  Enter the following command in the Web Shell:

      ``tail -f /var/log/squid3/access.log``

-  Visit a few secure (HTTPS) websites (non-banking) using Firefox on the Windows 10 Desktop and confirm that access is still being logged. You should see log entries of the sites and URLs visited but the username field (immediately after the URI) will be blank ("-"), similar to the example below:

   |proxy-access-log-nouser|

-  SSL Orchestrator does not pass authenticated usernames to a proxy service unless explicitly configured to do so. In the next step you will enable this feature.

-  On SSL Orchestrator select **SSL Orchestrator > Configuration** from the Main menu on the left

-  Click **Services** on the horizontal menu and then click on **ssloS_SquidProxy**. The Summary page will load for the Squid proxy service.

-  Click the edit icon (|pencil|) to the right of **Service**

-  Scroll down the Service Properties screen and select the **Authentication Offload** checkbox. Doing so will cause SSL Orchestrator to inject an "X-Authenticated-User" header into the HTTP payload of traffic it directs to the Squid proxy service.

-  Click the **Save & Next** button and confirm by clicking the **OK** button in the pop-up that appears

-  The **Service Chain List** screen will load. Wait a moment for the yellow "Deploy" ribbon to appear. When it does, click the **Deploy** button.

-  Visit a few more secure (HTTPS) websites (non-banking) using Firefox on the Windows 10 Desktop. You should now see your username logged along with the HTTP requests you sent, similar to the example below:

   |proxy-access-log-mike|

.. |proxy-access-log-nouser| image:: ../images/proxy-access-log-nouser.png
   :width: 1076px
   :height: 118px
   :alt: Proxy Access Log
.. |pencil| image:: ../images/pencil.png
   :width: 20px
   :height: 20px
   :alt: Pencil Icon
.. |proxy-access-log-mike| image:: ../images/proxy-access-log-mike.png
   :width: 1100px
   :height: 118px
   :alt: Proxy Access Log with Mike's Username
