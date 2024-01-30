Testing the Inbound Gateway Deployment
================================================================================

You have now deployed an **Inbound Gateway Mode** SSL Orchestrator configuration with a traffic policy that steers decrypted traffic to a Service Chain containing an Inline L3 inspection service and an ICAP service. The next step is to test your application from a client environment and verify that decrypted traffic is visible to the inspection services.

You have effectively configured a routed (next hop) gateway at the BIG-IP that listens for all incoming addresses and forwards to the backend. An Internet client would resolve an application to an IP address **behind** the BIG-IP instance, potentially on another BIG-IP, or other application server. Assuming multiple applications exist behind the BIG-IP, TLS certificate handling can be done in two different ways:

- Using a single wildcard domain certificate matching all of the destination hosts. The **wildcard.f5labs.com** certificate used in this lab is applying this option. The lab client is configured to resolve the following hostnames to internal IPs:

  - gwapp1.f5labs.com
  - gwapp2.f5labs.com
  - gwapp3.f5labs.com

- Using separate entity certificates in the client-side TLS configuration. In this scenario, each additional certificate added in the **Enable HTTPS (Client-Side TLS)** drawer under the **Protocols & Profiles** configuration will also need one or more Server Names added. In this dialog, click the **Add Servers** option, click the **Start Adding** button, and then enter one or more names. This name maps to the Server Name Indication (SNI) value from the TLS ClientHello request coming from the client. The matching SNI (server name) defines which certificate is then presented to the client in the TLS handshake. One and only one of the certificates added MUST be set to **Use Default Server**, while all of the others must add one or more server names. The certificate with **Use Default Server** selected is the certificate that will be used if no other certificate matches the incoming client SNI.



Test Access to the HTTPS Application
--------------------------------------------------------------------------------

You will now test the HTTPS application by sending a command line **cURL** request to the BIG-IP Virtual Server.

#. In the **Client VM shell** (or a shell running in the Client VM desktop), enter the following commands to verify that the applications behind SSL Orchestrator are reachable:

   .. code-block:: text

      curl -vk https://gwapp1.f5labs.com
      curl -vk https://gwapp2.f5labs.com
      curl -vk https://gwapp3.f5labs.com


#. Under the **Ubuntu-Server** resource of the UDF Deployment tab, click on Access -> **Web Shell**. This will open a console shell window to the Server VM (in a separate browser tab).

   .. note::
      The **Ubuntu-Server** VM instance leverages a set of Docker containers that are running various tools to emulate real world inspection services. In order to view the traffic flowing through these services, you will need to connect to the Docker containers.


#. **Capture traffic on the ICAP interface**: The ICAP service container does not have any capture tools installed, but you can still access the container's dedicated interface from the **Ubuntu-Server** instance.

   .. code-block:: text

      sudo tcpdump -lnni ens6.50

   .. note::
      An ICAP server will not receive encrypted traffic, so by design traffic to the **gwapp3.f5labs.com** URL per the above policy will not be seen in ICAP captures. To see this encrypted traffic, use the Inline Layer 3 inspection service.


#. The **Inline Layer 3 inspection service** runs inside a container named **layer3**. Execute the following commands to access the container shell and perform a tcpdump packet capture on the service's **inbound** interface (eth1):

   .. code-block:: text

      docker exec -it layer3 /bin/bash
      tcpdump -lnni eth1 -Xs0

   The ``-Xs0`` (capital 'x', lowercase 's', zero) flag allows you to view the unencrypted payload.


#. From the **Client VM Web Shell**, test the BIG-IP application using each of the three provided hostnames: **gwapp1.f5labs.com, gwapp2.f5labs.com, and gwapp3.f5labs.com**. The tcpdump packet capture should show clear text (decrypted) traffic to the first two hosts, and encrypted traffic to the third host.


|

.. attention::
   This is the end of the lab module.
