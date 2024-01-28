Creating an Inbound Application Deployment
================================================================================


You have completed the create of SSL Orchestrator Inspection Services, Service Chain, and Traffic Policy. The next step is to apply this to an application.


Create an Inbound Application with SSL Orchestrator Policy
--------------------------------------------------------------------------------

#. In the BIG-IP Central Manager GUI, click on the **Workspace** icon to show the **Workspace Menu**.

#. Click on **Applications** to navigate to the Applications workspace. You should see the application that you created in the previous lab module.

   .. image:: ./images/second-app-0a.png


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
   - Click on the **Monitor Type** field to show the available options.
   - De-select **http** and select **icmp**
   - Click outside of the list to use the selected options.

#. Click on **Virtual Servers** to switch to back to the Virtual Server configuration options.

   - Enter ``my-app2-sslo`` in the **Virtual Server Name** field.
   - In the **Pool** field, select the **my-pool** pool.
   - Change the **Virtual Port** to ``443`` (default value was **80**)

#. In the **Protocols & Profiles** field, click on the **edit icon** to open the settings panel.

#. Enable (toggle on) the **Enable HTTPS (Client-Side TLS)** option to show additional settings.

   - Click on the **Add** button to open the configuration panel.
   - In the **Add Client-Side TLS** panel, enter ``wildcard.f5labs.com`` as the name
   - Select **wildcard.f5labs.com** in the **RSA certificate** dropdown list box. This certificate was pre-installed in your lab environment.
   - Click on the **Save** button to close the panel.

#. Scroll down to see the other **Protocol & Profiles** options.

#. Enable (toggle on) the **Enable Server-side TLS** option.

#. Ensure that the **Enable SNAT** and **Enable Auto SNAT** options are enabled (default).

#. Disable (toggle off) the **Enable Connection Mirroring** option.

#. Click on the **Save** button to the close the **Protocols & Profiles** panel. 

   Notice that the **TLS** and **HTTPS** badges were added, and **MIRRORING** was removed.


#. In the **Security Policies** column, click the **edit icon** to open the **Security Profiles** panel.

   .. image:: ./images/second-app-0.png


#. Enable (toggle on) the **Use an SSL Orchestrator Policy** option and then select your SSL Orchestrator traffic policy.

   .. image:: ./images/second-app-1.png

#. Click **Save** to close the panel.

   Notice that the **SSLO** label now shows in the **Security Policies** column.

   .. image:: ./images/second-app-2.png

#. At the bottom right corner, click on the **Review & Deploy** button to open the **Deploy** panel.

   - Click on the **Start Adding** button.
   - Select the instance named **bigip-next.f5labs.com**.
   - Click on the **+ Add to List** button.

#. In the **Virtual Address** field, enter ``10.1.10.21`` .
   
#. In the **Members** column, click on the down arrow and then click **+ Pool Members** to open the settings panel.

   - Click on the **+ Add Row** button 3 times to create empty entries.

   - Add the following entries:

      - Name: ``mbr-192.168.100.11``, IP Address: ``192.168.100.11``
      - Name: ``mbr-192.168.100.12``, IP Address: ``192.168.100.12``
      - Name: ``mbr-192.168.100.13``, IP Address: ``192.168.100.13``

   - Click on the **Save** button to close the Pool settings panel.


#. In the **Configure** column, click the **edit icon**. 

   - Enable (toggle on) the **Enable VLANs to listen on** option and select **clientside**.
   - Click **Save**.


#. Click on the **Validate All** button to validate the pending configuration changes.

   .. image:: ./images/second-app-3.png


#. If validation is successful, you will see **Validated** and a link to **View Results**. You may optionally click on the link to view the configuration, then click **Exit** to close the results panel.

#. Click on the **Deploy Changes** button. Then, click on the **Yes, Deploy** button to send the application configuration to the BIG-IP Next instance.


When the deployment has completed, the **Application Services** dashboard will show the status of the application.

   .. image:: ./images/second-app-4.png
