Deploy SaaS Tenant Isolation Objects
================================================================================

SaaS Tenant Isolation Script
--------------------------------------------------------------------------------

**SaaS Tenant Isolation** functionality is a Service Extension for SSL Orchestrator. An installation script automates the creation of the configuration objects needed to implement this functionality.

- The script creates the following objects:
   - F5_SaaS-Tenant-Isolation Inspection Service - the SaaS Tenant Isolation Service Extension to interact with decrypted traffic flows.
   - Internal Virtual Server to act as the target for the SaaS Tenant Isolation Inspection Service.
   - SaaS Tenant Isolation iRule - injects the SaaS Tenant Isolation prompts, as well as optional logging.


Download the Installation Script
--------------------------------------------------------------------------------

#. From the UDF **Deployment** tab, access the Web Shell of the **BIG-IP SSLO** resource. This will open a new browser tab with an SSH session (logged in as the **root** user).

   .. image:: images/udf-sslo-webshell-1.png
      :align: left


#. Change Directory to the /tmp directory:

   .. code-block:: text

      cd /tmp


#. Download the installation script:      

   .. code-block:: text

      curl -sk https://raw.githubusercontent.com/f5devcentral/sslo-service-extensions/refs/heads/main/saas-tenant-isolation/saas-tenant-isolation-installer.sh -o saas-tenant-isolation-installer.sh


   .. tip::

      Click the **copy** icon in the URL text box above and paste it into the **BIG-IP SSLO - Web Shell** session. If your local machine is Windows, press the <CTRL>-<SHIFT>-V combination to paste.


Run the Installation Script
--------------------------------------------------------------------------------

#. Make the installation script executable:

   .. code-block:: text

      chmod +x saas-tenant-isolation-installer.sh


#. Create a BASH environment variable containing the BIG-IP username and password:

   .. code-block:: text

      export BIGUSER='admin:admin'


#. Run the installation script to create all of the SaaS Tenant Isolation objects:

   .. code-block:: text

      ./saas-tenant-isolation-installer.sh


   .. image:: images/udf-saas-isolation-install.png
      :align: left



Verify Object Creation
--------------------------------------------------------------------------------

#. From the UDF **Deployment** tab, access the TMUI of the **BIG-IP SSLO** resource. This will open a new browser tab with a GUI session.  As before, login with **admin** / **admin**.

    .. image:: images/udf-sslo-tmui.png
      :align: left




#. Navigate to **Local Traffic > iRules** and verify that the following iRules are present.

   - **saas-tenant-irule**

   .. image:: images/udf-irule-verify.png
      :align: left


#. Navigate to **SSL Orchestrator > Configuration**. In the diagram, you should see the **ssloS_F5_SaaS-Tenant-Isolation** Inspection Service icon (along with the F5_UC that you previously deployed).

#. Click on the **Services** tab and verify that the **ssloS_F5_SaaS-Tenant-Isolation** Inspection Service is present.

   .. image:: images/udf-saas-isolation-install-verify.png
      :align: left



This completes the installation of the configuration objects needed to support the **SaaS Tenant Isolation** Service Extension. In a later step, you will add the resulting **ssloS_F5_SaaS-Tenant-Isolation** Service to the existing Service Chain.
