Deploying an Application
==============================================================================

Install Certificates and Keys
--------------------------------------------------------------------------------

With the BIG-IP Next instance activated, follow these steps to install the
certificate and private key needed to host an HTTPS application.

#. In the top left corner of the CM UI, click the workspace menu tool (9
   dots) and click **Applications**, then click **Certificates & Keys**
   in the left menu.

#. Click the **Add Certificates** button, then in the following drawer
   select **Import a Certificate**.

   - **Name**: Create New. Enter a unique name.

   - **Type**: Certificate & Key

   - **Source**: Import

   - **Certificate**: Import the certificate.

   - **Key**: Import the private key.

   - **Key Security Type**: Normal

#. Click the **Save** button.


Create an HTTPS Application
--------------------------------------------------------------------------------

It's now time to create a simple HTTPS application. Follow these steps:

#. In the Applications UI, click **My Application Services** under the
   **Applications** menu. Click the **Start Adding Apps** button.

#. In the Add Application drawer, enter a unique application name and
   click the **Start Creating** button.

#. Optionally add a description and then click the **Start Creating**
   button.

#. First navigate to the **Pools** column and enter a unique name for
   your web server pool and change the **Service Port** to 443.

#. Navigate back to the **Virtual Servers** column and enter a unique
   name for your new application. Select the previously created pool,
   and then change the **Virtual Port** to 443.

#. In the **Protocols & Profiles** column, click the tool icon to open a
   new Protocols & Profiles drawer. Enable (toggle) the **Enable HTTPS
   (Client-Side TLS)** option, then select the previously imported
   certificate. Also enable (toggle) the **Enable Server-side TLS**
   option. Click the **Save** button.

#. Click the **Review & Deploy** button in the bottom right of the
   application drawer.

#. In the new **Deploy** drawer click the **Start Adding** button and
   select the BIG-IP Next instance. Click the **+ Add to List** button.

#. In the **Deploy** drawer, now enter the **Virtual Address**
   (10.1.10.20). In the **Members** column click the down arrow and
   click **+ Pool Members**.

#. In the new pool member drawer, click the **+ Add Row** button three
   times, then add the following entries and then click the **Save**
   button:

   - Name: ``mbr_192.168.100.11``, IP Address: ``192.168.100.11``

   - Name: ``mbr_192.168.100.12``, IP Address: ``192.168.100.12``

   - Name: ``mbr_192.168.100.13``, IP Address: ``192.168.100.13``

#. Click the **Deploy Changes** button to push the application
   definition to the BIG-IP Next instance.


Log into the Client and Test Access to the HTTPS Application
--------------------------------------------------------------------------------

Congratulations! You've just deployed a simple HTTPS application on
BIG-IP Next. The next step is to test your application from a client
environment. The UDF lab provides a unique client VM instance running a
version of Ubuntu Linux, access to an interactive shell for command line
testing, and a user desktop to run GUI browsers and other tools. Follow
these options to access either the client command line shell or desktop
GUI in the UDF lab:

-  **To access the Client VM shell**: In the UDF deployment window, find
   the Ubuntu **Client** instance and then find the “Web Shell” access
   option. This will open a console shell window to the client VM in a
   separate browser tab.

-  **To access the Client VM desktop**: In the UDF deployment window,
   find the Ubuntu **Server** instance and then find the “WebRDP” access
   option. This opens a new browser window to an instance of Guacamole
   running on the Ubuntu server with remote desktop access to the client
   desktop GUI. Enter the username (user) and password (user) to access
   the client desktop through the browser window.

The simplest test of the HTTPS application can be done with a command
line cURL request. In the VM shell, or a shell running in the client
desktop, enter the following command:

.. code-block:: bash

   curl -vk https://10.1.10.20

If successful, you will see the full HTML output from the web servers
behind the BIG-IP Next HTTPS application. You can perform the same test
in a client desktop browser using: https://www.f5labs.com.


|

.. attention::
   This is the end of the lab module.
