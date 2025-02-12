Testing the Deployment
================================================================================

You will now test the SSL Orchestrator Topology and perform an attack against the applications to see the difference in behavior between the two Service Chains.


Access the Ubuntu-client Desktop
--------------------------------------------------------------------------------

#. From the **Deployment** tab in the UDF console, select **ACCESS > WEBRDP** for the **Ubuntu-Server** resource (*Components > Ubuntu-Server > ACCESS > WEBRDP*).

   A new tab will open and present the Guacamole login screen.

   .. note::

      The **Guacamole** application is hosted on the **Server** machine, but creates an RDP connection to the **Client** machine.


#. Log in as ``user`` with password ``user``.

   .. image:: images/webrdp-login-1.png
      :align: left

#. The first time that you connect to the desktop, you will be prompted for permission to **"See text and images copied to the clipboard"**. Click on the **Allow** button to close the dialog box.


You should now see the desktop of the **Client** machine.

   .. image:: images/webrdp-login-2.png
      :align: left



Attack Juiceshop Application #1 (jsapp1.f5labs.com)
--------------------------------------------------------------------------------

You will now perform a SQL Injection (SQLi) attack to test the inspection services associated with **jsapp1**.

#. Launch the **Firefox** browser and browse to the following URL:

   .. code-block:: text

      https://jsapp1.f5labs.com/rest/products/search?q=qwert')) UNION SELECT id, email, password, '4', '5', '6', '7', '8', '9' FROM Users--


   .. tip::

      Click the **copy** icon in the URL text box above and paste it into the Ubuntu-Client browser address bar.


#. If you see a TLS security warning, accept it and continue. The lab's private Certificate Authority certificate might not be installed in **Firefox**.


You should see that the attack reached the application server and returned unauthorized data from user account database. This is a major vulnerability in the application.

   .. image:: images/sqli-1.png
      :align: left


Recall that **Service Chain 1** contained only the IPS service, which isn't sufficient to protect against this type of attack.


Attack Juiceshop Application #2 (jsapp2.f5labs.com)
--------------------------------------------------------------------------------

You will now perform a SQL Injection attack to test the inspection services associated with **jsapp2**.

#. Launch the Firefox browser and browse to the following URL:

   .. code-block:: text

      https://jsapp2.f5labs.com/rest/products/search?q=qwert')) UNION SELECT id, email, password, '4', '5', '6', '7', '8', '9' FROM Users--

   |

   Recall that **Service Chain 2** contained both the **FireEye** and **F5 Advanced WAF** inspection services. This time, the attack was blocked by the WAF policy.

   .. image:: images/sqli-2.png
      :align: left


#. In the BIG-IP TMUI, navigate to **Security > Event Logs** to view the WAF violation details.

   .. image:: images/sqli-3.png
      :align: left

