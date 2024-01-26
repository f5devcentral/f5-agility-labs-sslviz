Testing the Inbound Application Deployment
================================================================================

You have now deployed an SSL Orchestrator HTTPS application with a traffic policy that steers decrypted traffic to an Inline L3 inspection service. The next step is to test your application from a client environment and verify that decrypted traffic is visible to the inspection service.


Test Access to the HTTPS Application
--------------------------------------------------------------------------------

You will now test the HTTPS application by sending a command line **cURL** request to the BIG-IP Virtual Server. 


#. In the **Client VM shell** (or a shell running in the Client VM desktop), enter the following command:

   .. code-block:: text

      curl -vk https://10.1.10.21

   You should see HTML payload of the web page returned.

#. Under the **Ubuntu-Server** resource of the UDF Deployment tab, click on Access -> **Web Shell**. This will open a console shell window to the Server VM (in a separate browser tab).

   .. note::
      The **Ubuntu-Server** VM instance leverages a set of Docker containers that are running various tools to emulate real world inspection services. In order to view the traffic flowing through these services, you will need to connect to the Docker containers.


#. The **Inline Layer 3 inspection service** runs inside a container named **layer3**. Execute the following command to access the container shell:

   .. code-block:: text

      docker exec -it layer3 /bin/bash


#. From inside the layer3 service, initiate a tcpdump packet capture on the service's **inbound** interface (eth1):

   .. code-block:: text

      tcpdump -lnni eth1 -Xs0

   
   The ``-Xs0`` (capital 'x', lowercase 's', zero) flag allows you to view the unencrypted payload.

|

   .. note::

      The Client VM has been configured to resolve hostnames **www.f5labs.com** and **test.f5labs.com** to the BIG-IP's VIP address.


#. From the **Client VM Web Shell**, test the BIG-IP application using the hostname **www.f5labs.com**. Enter:

   .. code-block:: text

      curl -vk https://www.f5labs.com

   The packet capture (tcpdump) running on the **layer3** service will show the decrypted HTML payload flowing across its inbound interface.

   .. image:: ./images/second-app-5.png


#. From the **Client VM Web Shell**, test the BIG-IP application using the hostname **test.f5labs.com.**. Enter:

   .. code-block:: text

      curl -vk https://test.f5labs.com

   Recall that you previously defined a traffic rule with a condition to bypass TLS decryption for **test.f5labs.com**. The packet capture (tcpdump) running on the **layer3** service will now show the encrypted payload flowing across its inbound interface.


|

.. attention::
   This is the end of the lab module.
