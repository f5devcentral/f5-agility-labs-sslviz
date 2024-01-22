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
   **Applications** menu.

#. Click the **Start Adding Apps** button.

#. In the **Add Application** drawer, enter ``my-app-1`` and an optional description. Then,
   click the **Start Creating** button.

#. Navigate to the **Pools** column and click on **+ Create**.

   #. Enter ``my_pool`` as the **Pool** name and change the **Service Port** to **443**.

   #. Change the **Monitor Type** to **icmp**.

#. Navigate back to the **Virtual Servers** column and enter ``my_app`` for your new application.

   #. Select the previously created pool and change the **Virtual Port** to **443**.

#. In the **Protocols & Profiles** column, click the tool icon to open the configuration
   settings drawer.

   #. Enable the **Enable HTTPS (Client-Side TLS)** option, then click on the **Add** button.

   #. In the **Add Client-Side TLS** drawer, enter ``wildcard.f5labs.com`` as the name and
      then select the **wildcard.f5labs.com** RSA certificate. This certificate was included as part of your lab environment.

   #. Enable the **Enable Server-side TLS** option.

   #. Enable the **Enable SNAT** and **Enable Auto SNAT** options.

   #. Disable the **Enable Connection Mirroring** option.

#. Click the **Save** button to the close the **Protocols & Profiles** drawer.

#. At the bottom right corner, click the **Review & Deploy** button to open the **Deploy** drawer:

   #. Click the **Start Adding** button and select the BIG-IP Next instance.

   #. Click the **+ Add to List** button.

   #. Enter the ``10.1.10.20`` in the **Virtual Address** field.

   #. In the **Members** column, click the down arrow and then click **+ Pool Members**.

   #. In the **New Pool Member** drawer, click the **+ Add Row** button 3 times to create additional entries.

   #. Add the following entries:

      - Name: ``mbr_192.168.100.11``, IP Address: ``192.168.100.11``

      - Name: ``mbr_192.168.100.12``, IP Address: ``192.168.100.12``

      - Name: ``mbr_192.168.100.13``, IP Address: ``192.168.100.13``

  #. Click the **Save** bottom to close the **Pool Member** drawer.

#. Click the **Deploy Changes** button to send the application
   definition to the BIG-IP Next instance.

