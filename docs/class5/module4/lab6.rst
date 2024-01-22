Testing the Inbound Application Deployment
================================================================================


Test Access to the HTTPS Application
--------------------------------------------------------------------------------

You have just deployed an SSL Orchestrator HTTPS application on BIG-IP Next, with a traffic policy steering decrypted traffic to an Inline L3 and an ICAP inspection service. The next step is to test your application from a client environment. The UDF lab provides a unique client VM instance running a version of Ubuntu Linux, access to an interactive shell for command line testing, and a user desktop to run GUI browsers and other tools. Follow these options to access either the client command line shell or desktop GUI in the UDF lab:

- **To access the Client VM shell**: In the UDF deployment window, find the Ubuntu Client instance and then find the Web Shell access option. This will open a console shell window to the client VM in a separate browser tab.

- **To access the Client VM desktop**: In the UDF deployment window, find the Ubuntu Server instance and then find the WebRDP access option. This opens a new browser window to an instance of Guacamole running on the Ubuntu server with remote desktop access to the client desktop GUI. Enter the username (``user``) and password (``user``) to access the client desktop through the browser window.

The simplest test of the HTTPS application can be done with a command line cURL request. In the VM shell, or a shell running in the client desktop, enter the following command:

.. code-block:: text

   curl -vk https://10.1.10.21

If you prefer, the client has been configured to resolve the above IP address to **www.f5labs.com** and **test.f5labs.com**. Recall from the traffic rule creation that a condition was defined that does a TLS bypass on this second hostname. We will get into BIG-IP testing Debug Utility appendix, but for now an easy way to see traffic flowing to inspection services is at these inspection services.

#. **Access the Server VM shell**: In the UDF deployment window, find the Ubuntu **Server** instance and then find the Web Shell access option. This will open a console shell window to the server VM in a separate browser tab.

#. **Access the layer3 service container**: The consolidated lab architecture is a set of Docker containers running various utilities to emulate real world inspection services. The Inline Layer 3 inspection service is named **layer3**. To access this:

   .. code-block:: text

      docker exec -it layer3 /bin/bash


#. Initiate a tcpdump packet capture: From inside the layer 3 inspection service, initiate a tcpdump packet capture on the service's **inbound** interface:

   .. code-block:: text

      tcpdump -lnni eth1


#. Optionally add the ``-Xs0`` flag to the capture command to view the unencrypted payload.

   .. code-block:: text

      tcpdump -lnni eth1 -Xs0


#. Access the BIG-IP application using one of the two provided hostnames: www.f5labs.com or test.f5labs.com. The tcpdump packet capture will show this traffic flowing across the layer 3 service.





|

.. attention::
   This is the end of the lab module.
