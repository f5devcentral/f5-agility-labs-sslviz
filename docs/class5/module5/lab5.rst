Creating an Inbound Gateway Deployment
================================================================================


Create an Inbound Gateway Application with SSL Orchestrator Policy
--------------------------------------------------------------------------------

SSL Orchestrator inspection services, service chain, and traffic policy creation are now done, and it is time to apply this to a gateway application.

#. In the top left corner of the BIG-IP Central Manager (CM) UI, click on the **Workspace** icon to show the **Workspace Menu**.

#. Click on **Applications** to navigate to the Applications workspace. You should see the applications that you created in the previous lab modules.

#. Click on **+ Add Application** to open the **Add Application** panel.

#. Enter ``my-sslo-lab3-app`` in the **Application Service Name** field.

#. Click the **From Template** button.

#. Click on **Select Template** and then select **sslo-inbound-gateway-topology**.

#. Click on the **Start Creating** button to open the **Application Service Properties** panel.


#. Click **Start Creating** to open the **Virtual Servers** panel.

#. In the **Virtual Servers** box, enter ``my-service`` for the name of your new application
   and set the **Virtual Port** to ``443``. 

#. In the **Protocols & Profiles** field, click on the edit icon to open the settings panel.

#. Enable the **Enable HTTPS (Client-Side TLS)** option to show additional settings.

   - Click on the **Add** button to open the configuration panel.
   - In the **Add Client-Side TLS** panel, enter ``wildcard.f5labs.com`` as the name
   - Select **wildcard.f5labs.com** in the **RSA certificate** dropdown list box. This certificate was pre-installed in your lab environment.
   - Click on the **Save** button.
   - Click on the **Save** button to close the panel.

#. Scroll down to see the other **Protocol & Profiles** options.

#. Enable the **Enable Server-side TLS** option.

#. Ensure that the **Enable SNAT** and **Enable Auto SNAT** options are enabled (default).

#. Disable the **Enable Connection Mirroring** option.

#. Click on the **Save** button to the close the **Protocols & Profiles** panel. 

   Notice that the **TLS** and **HTTPS** badges were added, and **MIRRORING** was removed.


#. In the **Security Policies** column, click the edit icon to open the **Security Profiles** panel.

#. Enable the **Use an SSL Orchestrator Policy** option and then select your SSL Orchestrator traffic policy.

   .. image:: ./images/third-app-1.png

#. Click **Save** to close the panel.

   Notice that the **SSLO** label now shows in the **Security Policies** column.

   .. image:: ./images/third-app-2.png

#. At the bottom right corner, click on the **Review & Deploy** button to open the **Deploy** panel.

   - Click on the **Start Adding** button.
   - Select the instance named **bigip-next.f5labs.com**.
   - Click on the **+ Add to List** button.

#. In the **Deploy** panel, enter ``0.0.0.0/0`` for the **Virtual Address**. This will create a listener for all incoming addresses.

#. In the **Configure** column, click the edit icon. 

#. Enable the **Enable VLANs to listen on** option and select **clientside**.

#. Click **Save**.


   .. note::
      No pool or pool members are required for a gateway mode deployment.


#. Click on the **Validate All** button to validate the pending configuration changes.

   .. image:: ./images/third-app-3.png


#. If Validation is successful, click on the **Deploy Changes** button. Then, click on the **Yes, Deploy** button to send the application definition to the BIG-IP Next instance.

   After deployment, the **Application Services** dashboard will show the status of your application.

   .. image:: ./images/third-app-4.png

