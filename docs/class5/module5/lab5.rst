Creating an Inbound Gateway Deployment
================================================================================


Create an Inbound Gateway Application with SSL Orchestrator Policy
--------------------------------------------------------------------------------

SSL Orchestrator inspection services, service chain, and traffic policy creation are now done, and it is time to apply this to a gateway application.

#. In the top left corner of the CM UI, click the workspace menu tool (9 dots) and click **Applications**. An application may already exist from the previous lab, but in any case either click the **Start Adding Apps** button (no existing applications), or the **+ Create** button (existing applications).

#. In the **Add Application** drawer, enter ``my-sslo-lab3-app`` for the application name and select **From Template**.
 
#. Click the **Select Template** button and then select the **sslo-inbound-gateway-topology** and click the **Start Creating** button.

#. In the **Virtual Servers** box, enter ``my-service`` for the name of your new application
   and set the **Virtual Port** to ``443``. 

#. In the **Protocols & Profiles** column, click the tool icon to open a new **Protocols & Profiles** drawer.

   - Enable the **Enable HTTPS (Client-Side TLS)** option, then click the **Add** button.
   - In the **Add Client-Side TLS** drawer, enter ``wildcard.f5labs.com`` and select the
     **wildcard.f5labs.com** RSA Certificate.
   - Click the **Save** button.
   - Enable the **Enable Server-side TLS** option.
   - Enable the **Enable SNAT** and **Enable Auto SNAT** options.
   - Disable the **Enable Connection Mirroring** option.

#. Click the **Save** button in the **Protocols & Profiles** drawer.

#. In the **Security Policies** column, click the tool icon to open a new **Security Profiles** drawer.

#. Enable the **Use an SSL Orchestrator Policy** option and then select your SSL Orchestrator traffic policy.

#. Click **Save**.

#. Click the **Review & Deploy** button in the bottom right of the application drawer.

#. In the new **Deploy** drawer, click the **Start Adding** button and select the BIG-IP Next instance.

#. Click the **+ Add to List** button.

#. In the **Deploy** drawer, enter ``0.0.0.0/0`` for the **Virtual Address**. This will create a listener for all incoming addresses.

#. In the **Configure** column, click the tool icon. 

#. Enable the **Enable VLANs to listen on** option and select **clientside**.

#. Click **Save**.

   .. note::
      No pool or pool members are required for a gateway mode deployment.

#. Click the **Deploy Changes** button to push the application definition to the BIG-IP Next instance.
