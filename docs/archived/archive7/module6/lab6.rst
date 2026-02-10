Testing the API-based Deployment
================================================================================

You will now send some traffic to the applications and view the decrypted payloads flowing across inspection services.


Test Access to the HTTPS Application
--------------------------------------------------------------------------------

You will now test the HTTPS application by sending a command line **cURL** request to the BIG-IP Virtual Server. 


#. In the **Client VM shell** (or a shell running in the Client VM desktop), enter the following command:

   .. code-block:: text

      curl -vk https://10.1.10.22

   You should see HTML payload of the web page returned.


#. Under the **Ubuntu-Server** resource of the UDF Deployment tab, click on Access -> **Web Shell**. This will open a console shell window to the Server VM (in a separate browser tab).

#. Observe decrypted traffic to the TAP inspection device by initiating a tcpdump packet
   capture: The **TAP** interface is **ens7** directly on the host server VM:

   .. code-block:: text

      tcpdump -lnni ens7 -Xs0

#. In the **Client VM shell** (or a shell running in the Client VM desktop), send another cURL request:

   .. code-block:: text

      curl -vk https://10.1.10.22

   You should see decrypted traffic in the tcpdump packet capture (in the Server VM shell).

