Deploying an Application
==============================================================================

Install Certificates and Keys
--------------------------------------------------------------------------------

With the BIG-IP Next instance activated, follow these steps to install the
certificate and private key needed to host an HTTPS application.

#. In the top left corner of the CM UI, click on the workspace menu tool (9
   dots) and click **Applications**, then click **Certificates & Keys**
   in the left menu.

#. Click on the **Add Certificates** button, then in the following panel
   select **Import a Certificate**.

   - **Name**: Create New. Enter a unique name.

   - **Type**: Certificate & Key

   - **Source**: Import

   - **Certificate**: Import the certificate.

   - **Key**: Import the private key.

   - **Key Security Type**: Normal

#. Click on the **Save** button.


Create an HTTPS Application
--------------------------------------------------------------------------------

It's now time to create a simple HTTPS application. Follow these steps:

#. In the Applications UI, click on **My Application Services** under the
   **Applications** menu.

   .. image:: ./images/applications-menu.png

#. Click on the **Start Adding Apps** button to open the **Add Application** panel.

#. Enter ``my-app-1`` in the **Application Service Name** field.

#. Leave the **Application Service** type selection as **Standard** (default).

#. Click on the **Start Creating** button to open the **Application Service Properties** panel.

#. Enter ``My first application`` in the **Description** field.

#. Click on the **Start Creating** button to reveal the **Virtual Server** and **Pool** configuration options.

#. Click on **Pools** to switch to reveal Pool configuration options.

#. Click on **+ Create** to add a new Pool.

   - Enter ``my-pool`` in the **Pool Name** field.
   - Change the **Service Port** to ``443`` (default value was **80**)
   - In the **Monitor Type** field, click on the down arrow to show the available options.
   - Deselect **http** and select **icmp**
   - Click outside of the list to use the selected options.

#. Click on **Virtual Servers** to switch to back to the Virtual Server configuration options.

   - Enter ``my-app`` in the **Virtual Server Name** field.
   - In the **Pool** field, select the **my-pool** pool.
   - Change the **Virtual Port** to ``443`` (default value was **80**)

#. In the **Protocols & Profiles** field, click on the edit icon to open the settings panel.

#. Enable the **Enable HTTPS (Client-Side TLS)** option to show additional settings.

   - Click on the **Add** button to open the configuration panel.
   - In the **Add Client-Side TLS** panel, enter ``wildcard.f5labs.com`` as the name
   - Select **wildcard.f5labs.com** in the **RSA certificate** dropdown list box. This certificate was pre-installed in your lab environment.
   - Click on the **Save** button to close the panel.

#. Scroll down to see the other **Protocol & Profiles** options.

#. Enable the **Enable Server-side TLS** option.

#. Ensure that the **Enable SNAT** and **Enable Auto SNAT** options are enabled (default).

#. Disable the **Enable Connection Mirroring** option.

#. Click on the **Save** button to the close the **Protocols & Profiles** panel. 

   Notice that the **TLS** and **HTTPS** badges were added, and **MIRRORING** was removed.

#. At the bottom right corner, click on the **Review & Deploy** button to open the **Deploy** panel.

   - Click on the **Start Adding** button.
   - Select the instance named **bigip-next.f5labs.com**.
   - Click on the **+ Add to List** button.
   - Enter ``10.1.10.20`` in the **Virtual Address** field.

#. In the **Members** column, click on the down arrow and then click **+ Pool Members** to open the settings panel.

   - Click on the **+ Add Row** button 3 times to create empty entries.

   - Add the following entries:

      - Name: ``mbr-192.168.100.11``, IP Address: ``192.168.100.11``

      - Name: ``mbr-192.168.100.12``, IP Address: ``192.168.100.12``

      - Name: ``mbr-192.168.100.13``, IP Address: ``192.168.100.13``

   - Click on the **Save** button to close the Pool settings panel.

#. Click on the **Validate All** button to validate the pending configuration changes.

#. Once successful, click on the **Deploy Changes** button and then the **Yes, Deploy** 
   button to send the application definition to the BIG-IP Next instance.

