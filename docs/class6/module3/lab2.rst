Deploy User Coaching Objects
================================================================================

User Coaching Script
--------------------------------------------------------------------------------

**User coaching** functionality is a Service Extension for SSL Orchestrator. An installation script automates the creation of the configuration objects needed to implement this functionality.

The script creates the following objects:

   - F5_UC Inspection Service - the user coaching Service Extension to interact with decrypted traffic flows.
   - User coaching iRule - injects the user blocking and coaching prompts, as well as optional logging.
   - TLS fingerprinting iRule - determines if a user has already completed the user coaching flow.
   - user-coaching-html iFile - contains the user coaching HTML template.
   - user-blocking-html iFile - contains the user blocking HTML template


Download the Installation Script
--------------------------------------------------------------------------------

#. From the UDF **Deployment** tab, access the Web Shell of the **BIG-IP SSL Orchestrator** resource. This will open a new browser tab with an SSH session (logged in as the **root** user).

   .. image:: images/udf-sslo-webshell-1.png
      :align: left


#. Download the installation script:

   .. code-block:: text

      cd /tmp

      curl -sk https://raw.githubusercontent.com/f5devcentral/sslo-service-extensions/refs/heads/main/user-coaching/user-coaching-installer.sh -o user-coaching-installer.sh


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


#. Click on the **iFile List** tab and verify that the **user-coaching-html** and **user-blocking-html** iFiles are present.

   .. image:: images/uc-install-verify-2.png
      :align: left


#. Navigate to **SSL Orchestrator > Configuration**. In the diagram, you should see the **ssloS_F5_UC** Inspection Service icon (along with the others that you previously deployed).

#. Click on the **Services** tab and verify that the **ssloS_F5_UC** Inspection Service is present.

   .. image:: images/uc-install-verify-3.png
      :align: left

|


This completes the installation of the configuration objects needed to support the **user coaching** function. In a later step, you will add the resulting **ssloS_F5_UC** inspection Service to a decrypted traffic Service Chain and add the **user-coaching-ja4t-rule** iRule to the L3 Outbound Topology's Interception Rule.

