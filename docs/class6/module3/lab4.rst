Verify Outbound Topology Functionality
================================================================================

Route Client Traffic via BIG-IP SSL Orchestrator
--------------------------------------------------------------------------------

In order to route outbound traffic through the BIG-IP SSL Orchestrator, you will need to change the default gateway on the **Ubuntu-Client** machine.

#. Return to the **Ubuntu-Client** RDP tab (originally launched from the **Ubuntu-Server > WEBRDP** link).

#. Click on the **Terminal** icon at the bottom of the screen to open a new Terminal shell session.

   .. image:: ./images/ubuntu-route-1.png
      :align: left


#. Enter ``sudo ip route change default via 10.1.10.7`` to change the default route.

#. When prompted, enter ``agility`` as the password.

#. Enter ``ip route`` to verify that the default route has changed.

   .. image:: ./images/ubuntu-route-2.png
      :align: left

#. Close the **Terminal** window.

|

Test Internet Access
--------------------------------------------------------------------------------

#. Close the **Firefox** browser window and restart the application.

#. Navigate to https://www.f5.com.

   .. Important::

      Do not continue if you cannot browse the Internet from the Ubuntu-Client machine. If you are not able to resolve this on your own, reach out to the lab instructor/assistants to help troubleshoot.

#. Hover the mouse pointer over the padlock icon on the address bar and verify that it displays **Verified by: f5labs.com**. This confirms that SSL Orchestrator is performing TLS interception (decrypt & inspect) for outbound traffic. The TLS certificate for https://www.f5.com was forged by the subrsa CA certificate, which is trusted by the client machine.

   .. image:: ./images/l3outbound-test-1.png
      :align: left


#. Now, test a generative AI web site. Navigate to https://chatgpt.com and verify that it is accessible without any restrictions.

   .. note::

      You will test this again after enabling the **user coaching** functionality.

|


This completes the basic L3 Outbound Topology configuration.
