Creating an Inbound Gateway Deployment
================================================================================

You have created an SSL Orchestrator Inspection Service, a Service Chain, and a Traffic Policy. The next step is to apply this to an application.

Create an Inbound Gateway Application with SSL Orchestrator Policy
--------------------------------------------------------------------------------

#. In the BIG-IP Central Manager GUI, click on the **Workspace** icon to show the **Workspace Menu**.

#. Click on **Applications** to navigate to the Applications workspace. You should see the applications that you created in the previous lab module.

   .. image:: ./images/igm-app-0.png


#. Click on **+ Add Application** to open the **Add Application** panel.

#. Enter ``my-sslo-lab3-app`` in the **Application Service Name** field.

#. Click the **From Template** button.

   .. image:: ./images/igm-app-1.png


#. Click on **Select Template** and then select **sslo-inbound-gateway-topology**.

   .. image:: ./images/igm-app-2.png


#. Click on the **Start Creating** button to open the **Application Service Properties** panel.

#. Enter ``My SSLO inbound gateway application`` in the **Description** field.

#. Click **Start Creating** to reveal the **Virtual Server** configuration options.

#. In the **Virtual Servers** box, enter ``my-inbound-gw`` for the name of your new application
   and leave the **Virtual Port** set to ``0``. 

   .. image:: ./images/igm-app-3.png

   .. important::
      No Pool is configurable for an **Inbound Gateway Mode** deployment.


#. In the **Protocols & Profiles** field, click on the **edit icon** to open the settings panel.

#. Enable (toggle on) the **Enable HTTPS (Client-Side TLS)** option to show additional settings.

   - Click on the **Add** button to open the configuration panel.
   - In the **Add Client-Side TLS** panel, enter ``wildcard.f5labs.com`` as the name
   - Select **wildcard.f5labs.com** in the **RSA certificate** dropdown list box. This certificate was pre-installed in your lab environment.
   - Click on the **Save** button to close the panel.

#. Scroll down to see the other **Protocol & Profiles** options.

#. Enable (toggle on) the **Enable Server-side TLS** option.

#. Ensure that the **Enable SNAT** and **Enable Auto SNAT** options are enabled (default).

#. Click on the **Save** button to the close the **Protocols & Profiles** panel. 

   Notice that the **TLS** and **HTTPS** labels were added.

   .. image:: ./images/igm-app-4.png


#. In the **Security Policies** column, click the **edit icon** to open the **Security Profiles** panel.

#. Enable (toggle on) the **Use an SSL Orchestrator Policy** option and then select your SSL Orchestrator traffic policy.

   .. image:: ./images/igm-app-5.png

#. Click **Save** to close the panel.

   Notice that the **SSLO** label now shows in the **Security Policies** column.

   .. image:: ./images/igm-app-6.png

#. At the bottom right corner, click on the **Review & Deploy** button to open the **Deploy** panel.

   - Click on the **Start Adding** button.
   - Select the instance named **bigip-next.f5labs.com**.
   - Click on the **+ Add to List** button.

#. In the **Virtual Address** field, enter ``0.0.0.0/0``.
 
   .. important::
      This will create a listener for all incoming addresses.

      Also note that the Pool field is empty.

   .. image:: ./images/igm-app-7.png


#. In the **Configure** column, click the **edit icon** to open a panel with additional settings.

   - Enable (toggle on) the **Enable VLANs to listen on** option
   - Select **clientside**.

   .. image:: ./images/igm-app-8.png

#. Click on the **Save** button to return to the **Deploy** screen.

#. Click on the **Validate All** button to validate the pending configuration changes.

#. If validation is successful, you will see **Validated**.

#. [Optional] Click on the **View Results** link to view the configuration and then click **Exit** to close the results panel.

   .. image:: ./images/igm-app-9.png


#. Click on the **Deploy Changes** button. Then, click on the **Yes, Deploy** button to send the application configuration to the BIG-IP Next instance.


When the deployment has completed, the **Application Services** dashboard will show the status of the new application.

   .. image:: ./images/igm-app-10.png
