Testing the Inbound Gateway Deployment
================================================================================


Test Access to the HTTPS Application
--------------------------------------------------------------------------------

What you've effectively configured is a routed (next hop) gateway at the BIG-IP that listens for all incoming addresses and forwards to the backend. An Internet client would resolve an application to an IP address **behind** the BIG-IP instance, potentially on another BIG-IP, or other application server. Assuming multiple applications exist behind the BIG-IP, TLS certificate handling can be handled in two different ways:

- Using a single wildcard domain certificate matching all of the destination hosts. The **wildcard.f5labs.com** certificate used in this lab is applying this option. The lab client is configured to resolve the following hostnames to internal IPs:

  - gwapp1.f5labs.com
  - gwapp2.f5labs.com
  - gwapp3.f5labs.com

- Using separate entity certificates in the client-side TLS configuration. In this scenario, each additional certificate added in the **Enable HTTPS (Client-Side TLS)** drawer under the **Protocols & Profiles** configuration will also need one or more Server Names added. In this dialog, click the **Add Servers** option, click the **Start Adding** button, and then enter one or more names. This name maps to the Server Name Indication (SNI) value from the TLS ClientHello request coming from the client. The matching SNI (server name) defines which certificate is then presented to the client in the TLS handshake. One and only one of the certificates added MUST be set to **Use Default Server**, while all of the rest must add one or more server names. The certificate with **Use Default Server** selected is the certificate that will be used if no other certificate matches the incoming client SNI.

The UDF lab provides a unique client VM instance running a version of Ubuntu Linux, access to an interactive shell for command line testing, and a user desktop to run GUI browsers and other tools. Follow these options to access either the client command line shell or desktop GUI in the UDF lab:

- **To access the Client VM shell**: In the UDF deployment window, find the Ubuntu **Client** instance and then find the **Web Shell** access option. This will open a console shell window to the client VM in a separate browser tab.

- **To access the Client VM desktop**: In the UDF deployment window, find the Ubuntu **Server** instance and then find the **WebRDP** access option. This opens a new browser window to an instance of Guacamole running on the Ubuntu server with remote desktop access to the client desktop GUI. Enter the username (``user``) and password (``user``) to access the client desktop through the browser window.

The simplest test of the HTTPS application can be done with a command line cURL request. In the VM shell, or a shell running in the client desktop, enter the following command:

.. code-block:: bash

   curl -vk https://gwapp1.f5labs.com
   curl -vk https://gwapp2.f5labs.com
   curl -vk https://gwapp3.f5labs.com

Recall from the traffic rule creation that a condition was defined that does a TLS bypass on this third hostname. We will get into BIG-IP testing Debug Utility appendix, but for now an easy way to see traffic flowing to inspection services is at these inspection services.

#. **Access the Server VM shell**: In the UDF deployment window, find the Ubuntu **Server** instance and then find the **Web Shell** access option. This will open a console shell window to the server VM in a separate browser tab.

#. **Capture traffic on the ICAP interface**: The ICAP service container does not have any capture tools installed, but you can still access the container's dedicated interface from the **Server** instance.

   .. code-block:: bash

      sudo tcpdump -lnni ens6.50

#. **Capture traffic from the Inline L3 service**: An ICAP will not receive encrypted traffic, so by design traffic to the **gwapp3.f5labs.com** URL per the above policy will not be seen in ICAP captures. To see this encrypted traffic, use the Layer 3 service as described in Lab2:

   .. code-block:: bash

      docker exec -it layer3 /bin/bash
      tcpdump -lnni eth1


Access the BIG-IP application using one of the three provided hostnames: **gwapp1.f5labs.com, gwapp2.f5labs.com, and gwapp3.f5labs.com**. The tcpdump packet capture should show clear text (unencrypted) traffic to the first two hosts, and encrypted traffic to the third host.





|

.. attention::
   This is the end of the lab module.
