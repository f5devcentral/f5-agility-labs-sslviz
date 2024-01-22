Creating an Inbound Application Deployment
================================================================================


Create an Inbound Application with SSL Orchestrator Policy
--------------------------------------------------------------------------------

SSL Orchestrator inspection services, service chain, and traffic policy creation are now done, and now it is time to apply this to an application.

#. In the top left corner of the CM UI, click the workspace menu tool (9 dots) and click **Applications**. An application may already exist from the previous lab, but in any case either click the **Start Adding Apps** button (no existing applications), or the **+ Create** button (existing applications).

#. In the **Add Application** drawer, enter ``my-sslo-lab2-app`` for the application name and and optional description.

#. Click the **Start Creating** button.

#. First navigate to the **Pools** column and enter ``my-pool`` for the name of your web server pool and change the **Service Port** to ``443``.

#. Change the **Monitor Type** to **icmp**.

#. Navigate back to the **Virtual Servers** column and enter ``my-server`` for the name of your new application.

#. Select the previously created pool, and then change the **Virtual Port** to ``443``.

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

#. Enable the **Use an SSL Orchestrator Policy** option and then select your SSL Orchestrator traffic policy

#. Click **Save**.

#. Click the **Review & Deploy** button in the bottom right of the application drawer.

#. In the new **Deploy** drawer, click the **Start Adding** button and select the BIG-IP Next instance.

#. Click the **+ Add to List** button.

#. In the **Deploy** drawer, enter ``10.1.10.21`` for the **Virtual Address**.

#. In the **Members** column, click the down arrow and click **+ Pool Members**.

#. In the **new pool member** drawer, click the **+ Add Row** button **three** times, then add the following entries:

   - Name: ``mbr_192.168.100.11``, IP Address: ``192.168.100.11``
   - Name: ``mbr_192.168.100.12``, IP Address: ``192.168.100.12``
   - Name: ``mbr_192.168.100.13``, IP Address: ``192.168.100.13``

#. Click the **Save** button.

#. In the **Configure** column, click the tool icon. 

#. Enable the **Enable VLANs to listen on** option and select **clientside**

#. Click **Save**.

#. Click the **Deploy Changes** button to push the application definition to the BIG-IP Next instance.
