Deploy User Coaching Objects
================================================================================

User Coaching Script
--------------------------------------------------------------------------------

**User coaching** functionality is an extension to SSL Orchestrator. An **SSLO User Coaching** script automates the creation of the configuration objects needed to enable this functionality.

The script creates the following objects:

   - Inspection Service - faciliates the user coaching functionality for decrypted outbound SSO Orchestrator flows.
   - iFile - contains the user coaching form HTML template
   - User coaching iRule - injects the user coaching prompt and justificiation input form.
   - TLS fingerprinting iRule - determines if a user has already completed the user coaching flow for risk web sites.


Download the Installation Script
--------------------------------------------------------------------------------

#. From the UDF **Deployment** tab, access the Web Shell of the **BIG-IP SSL Orchestrator** resource. This will open a new browser tab with an SSH session (logged in as the **root** user).

   .. image:: images/udf-sslo-webshell-1.png
      :align: left


#. Download the installation script:

   .. code-block:: text

      cd /tmp

      curl -sk https://raw.githubusercontent.com/kevingstewart/sslo-user-coaching/refs/heads/main/user-coaching-installer.sh -o user-coaching-installer.sh


   .. tip::

      Click the **copy** icon in the URL text box above and paste it into the **Ubuntu-Client - Web Shell** session. If your local machine is Windows, press the <CTRL>-<SHIFT>-V combination to paste.



Run the Installation Script
--------------------------------------------------------------------------------

#. Make the installation script executable:

   .. code-block:: text

      chmod +x user-coaching-installer.sh


#. Create a BASH environment variable containing the BIG-IP username and password:

   .. code-block:: text

      export BIGUSER='admin:admin'


#. Run the installation script to create all of the User Coaching objects:


   .. code-block:: text

      ./user-coaching-installer.sh


   .. image:: images/udf-sslo-webshell-2.png
      :align: left



Verify Object Creation
--------------------------------------------------------------------------------

#. Switch to your local web browser tab that contains the **BIG-IP TMUI**.


#. Navigate to **Local Traffic > iRules** and verify that the following iRules are present.

   - user-coaching-ja4t-rule
   - user-coaching-rule

   .. image:: images/uc-install-verify-1.png
      :align: left


#. Click on the **iFile List** tab and verify that the **user-coaching-html** iFile is present.

   .. image:: images/uc-install-verify-2.png
      :align: left


#. Navigate to **SSL Orchestrator > Configuration** to see the **Topologies** tab. You should see the **ssloS_F5_UC** Inspection Service (along with the others that you previously deployed) in the diagram above.

#. Click on the **Services** tab and verify that the **ssloS_F5_UC** Inspection Service is present.

   .. image:: images/uc-install-verify-3.png
      :align: left

|


This completes the installation of the configuration objects needed to support the **user coaching** function. In a later step, you will add the resulting **ssloS_F5_UC** inspection Service to a decrypted traffic Service Chain and add the **user-coaching-ja4t-rule** iRule to the L3 Outbound Topology's Interception Rule.

