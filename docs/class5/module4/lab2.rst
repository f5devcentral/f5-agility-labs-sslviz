Defining an Inspection Service
================================================================================

The first step in this journey is to create the SSL Orchestrator inspection services. As previously noted, an inspection service will have network attributes that are specific to a BIG-IP Next instance (i.e., interfaces, VLANs, self-IPs). When creating an inspection service in CM, you will deploy these direct to the BIG-IP Next instance before the application is defined.


Create an Inline L3 Inspection Service
--------------------------------------------------------------------------------

#.	In the top left corner of the CM UI, click the workspace menu icon (9 dots) to see menu options.

#. Click on **Security**, then click on **Inspection Services** under **SSL Orchestrator**.

#.	Click the **Start Creating** button.

#.	In the **Create Inspection Service** drawer, select **Generic Inline L3** and then click the **Start Creating** button to open the configuration settings drawer.

   #.	Enter ``my-sslo-ngfw`` in the service name field.

   #. Enter ``next-gen firewall`` in the description field (optional).

   #. Click the **Save & Continue** button.

   #.	In the **Network** settings:

      #.	Enter ``sslo-insp-l3-in`` for the **To: VLAN**.

      #.	Enter ``sslo-insp-l3-out`` for the **From: VLAN**.

      #.	Select **ICMP** for the **Device Monitor**.

      #.	In the **Endppoints** section, click the **Start Adding** button.

      #. Enter ``198.19.64.30`` for the **IP Address**.

#. Click the **Review & Deploy** button.

#.	In the **Deploy Inspection Service** drawer, add the BIG-IP Next instance.

   #. Click the checkbox to the left of the assigned instance and then click the **Validate** button.

   #. If Validation is Successful, click the **Deploy Changes** button to push this inspection service configuration to the BIG-IP Next instance.

