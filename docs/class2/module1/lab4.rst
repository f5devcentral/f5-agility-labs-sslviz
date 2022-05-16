.. role:: red
.. role:: bred

Enable and test authentication offload
================================================================================

1.  Start a Web Shell to **Ubuntu18.04 Services** (**Systems > Ubuntu18.04 Services > ACCESS > Web Shell**). **MAKE SURE** you are accessing **Ubuntu18.04 Services** and not the **Ubuntu18.04 Client**.

   .. image:: ../images/udf-ubuntu-services-webshell.png
      :alt: Unbuntu Services Web Shell Access

2.  Enter the following commands in the Web Shell - **NOTE** You will need to type these commands into the **Web Shell** as it lacks copy-and-paste capabilities:

   .. code:: bash

      clear
      tail -f -n 0 /var/log/squid/access.log

3.  Visit a few secure (HTTPS) websites (non-banking) using Chrome on the Windows Client and confirm that access is still being logged. You should see log entries of the sites and URLs visited but the username field (immediately after the URI) will be blank ("-"), similar to the example below:

   |proxy-access-log-nouser|

|

SSL Orchestrator does not pass authenticated usernames to a proxy service unless explicitly configured to do so. In the next step you will enable this feature.

4.  On SSL Orchestrator select **SSL Orchestrator > Configuration** from the Main menu on the left

   |SSL-Orchestrator-Configuration|

5.  Click **Services** on the horizontal menu and then click on **ssloS_SquidProxy**. The Summary page will load for the Squid proxy service.

   |SSL-Configuration-Services|

6.  Click the edit icon (|pencil|) to the right of **Service**

   |SquidProxy-Service|

7.  Scroll down the Service Properties screen and select the **Authentication Offload** checkbox. Doing so will cause SSL Orchestrator to inject an "X-Authenticated-User" header into the HTTP payload of traffic it directs to the Squid proxy service.


.. image:: ../images/auth-offload.png
   :alt: Authentication Offload Option


8.  Click the **Save & Next** button and confirm by clicking the **OK** button in the pop-up that appears.

9.  The **Service Chain List** screen will load. Wait a moment for the yellow "Deploy" ribbon to appear. When it does, click the **Deploy** button.

   |Service-Chain-Deploy|

10.  Click **OK** to acknowledge the successful deployment.

11.  Visit a few more secure (HTTPS) websites (non-banking) using Chrome on the Windows Client. You should now see your username logged along with the HTTP requests you sent, similar to the example below:

   |proxy-access-log-mike|


12.  Press ``<CTRL+C>`` to stop the **tail** tool.


.. attention::
   This is the end of the lab module.



.. |proxy-access-log-nouser| image:: ../images/proxy-access-log-nouser.png
   :alt: Proxy Access Log

.. |pencil| image:: ../images/pencil.png
   :width: 20px
   :height: 20px
   :alt: Pencil Icon

.. |proxy-access-log-mike| image:: ../images/proxy-access-log-mike.png
   :alt: Proxy Access Log with Mike's Username

.. |SSL-Orchestrator-Configuration| image:: ../images/SSL-Orchestrator-Configuration.png
   :alt: SSL Orchestrator -> Configuration 

.. |SSL-Configuration-Services| image:: ../images/SSL-Configuration-Services.png
   :alt: SSL Configuration -> Services

.. |SquidProxy-Service| image:: ../images/SquidProxy-Service.png
   :alt: ssloS_SquidProxy - Services

.. |Service-Chain-Deploy| image:: ../images/Service-Chain-Deploy.png
   :alt: Service Chain Deploy