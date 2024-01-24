Creating an Inbound Application Deployment
================================================================================


Create an Inbound Application with SSL Orchestrator Policy
--------------------------------------------------------------------------------

SSL Orchestrator inspection services, service chain, and traffic policy creation are now done, and now it is time to apply this to an application.

#. In the top left corner of the BIG-IP Central Manager (CM) UI, click on the **Workspace** icon to show the **Workspace Menu**.

#. Click on **Applications** to navigate to the Applications workspace. You should see the application that you created in the previous lab.

#. Click on **+ Add Application** to open the **Add Application** panel.

#. Enter ``my-sslo-lab2-app`` in the **Application Service Name** field.

#. Leave the **Application Service** type selection as **Standard** (default).

#. Click on the **Start Creating** button to open the **Application Service Properties** panel.

#. Enter ``My second application`` in the **Description** field.

#. Click on the **Start Creating** button to reveal the **Virtual Server** and **Pool** configuration options.

#. Click on **Pools** to show the Pool configuration options.

#. Click on **+ Create** to add a new Pool.

   - Enter ``my-pool`` in the **Pool Name** field.
   - Change the **Service Port** to ``443`` (default value was **80**)
   - In the **Monitor Type** field, click on the down arrow to show the available options.
   - Deselect **http** and select **icmp**
   - Click outside of the list to use the selected options.

#. Click on **Virtual Servers** to switch to back to the Virtual Server configuration options.

   - Enter ``my-app2-sslo`` in the **Virtual Server Name** field.
   - In the **Pool** field, select the **my-pool** pool.
   - Change the **Virtual Port** to ``443`` (default value was **80**)

#. In the **Protocols & Profiles** field, click on the edit icon to open the settings panel.

#. Enable the **Enable HTTPS (Client-Side TLS)** option to show additional settings.

   - Click on the **Add** button to open the configuration panel.
   - In the **Add Client-Side TLS** panel, enter ``wildcard.f5labs.com`` as the name
   - Select **wildcard.f5labs.com** in the **RSA certificate** dropdown list box. This certificate was pre-installed in your lab environment.
   - Click on the **Save** button to close the panel.

#. In the **Security Policies** column, click the edit icon to open the **Security Profiles** panel.

#. Enable the **Use an SSL Orchestrator Policy** option and then select your SSL Orchestrator traffic policy.

   .. image:: ./images/second-app-1.png

#. Click **Save**.

   .. image:: ./images/second-app-2.png

#. At the bottom right corner, click on the **Review & Deploy** button to open the **Deploy** panel.

   - Click on the **Start Adding** button.
   - Select the instance named **bigip-next.f5labs.com**.
   - Click on the **+ Add to List** button.
   - Enter ``10.1.10.21`` in the **Virtual Address** field.


#. In the **Members** column, click on the down arrow and then click **+ Pool Members** to open the settings panel.

   - Click on the **+ Add Row** button 3 times to create empty entries.

   - Add the following entries:

      - Name: ``mbr-192.168.100.11``, IP Address: ``192.168.100.11``
      - Name: ``mbr-192.168.100.12``, IP Address: ``192.168.100.12``
      - Name: ``mbr-192.168.100.13``, IP Address: ``192.168.100.13``

   - Click on the **Save** button to close the Pool settings panel.


#. In the **Configure** column, click the edit icon. 

#. Enable the **Enable VLANs to listen on** option and select **clientside**.

#. Click **Save**.


#. Click on the **Validate All** button to validate the pending configuration changes.

   .. image:: ./images/second-app-3.png


#. Click the **Deploy Changes** button to push the application definition to the BIG-IP Next instance.

#. If Validation is successful, click on the **Deploy Changes** button. Then, click on the **Yes, Deploy** button to send the application definition to the BIG-IP Next instance.

   After deployment, the **Application Services** dashboard will show the status of your application.

   .. image:: ./images/second-app-4.png
