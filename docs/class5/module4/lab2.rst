Defining an Inspection Service
================================================================================

The first step in this journey is to create the SSL Orchestrator inspection services. As previously noted, an inspection service will have network attributes that are specific to a BIG-IP Next instance (i.e., interfaces, VLANs, self-IPs). When creating an inspection service in CM, you will deploy these direct to the BIG-IP Next instance before the application is defined.


Create an Inline L3 Inspection Service
--------------------------------------------------------------------------------

#. In the top left corner of the BIG-IP Central Manager GUI, click on the **Workspace** icon to show the **Workspace Menu**.

#. Click on **Security** to navigate to the Security workspace.

#. In the **SSL Orchestrator** menu, click on **Inspection Services**.

#. Click the **Start Creating** button.

   .. image:: ./images/service-1.png


#. In the **Create Inspection Service** panel, select **Generic Inline L3** and then click the **Start Creating** button.

   .. image:: ./images/service-2.png


#. In the **General Properties** section of the **Create Inspection Service: 'Generic L3'** panel:

   - Enter ``my-sslo-ngfw`` in the **Name** field.
   - Enter ``next-gen firewall`` in the **Description** field (optional).
   - Click the **Save & Continue** button.

   .. image:: ./images/service-3.png


#. In the **Network** settings:

   - Enter ``sslo-insp-l3-in`` in the **To: VLAN** > **VLAN Name** field.

   - Enter ``sslo-insp-l3-out`` in the **From: VLAN** > **VLAN Name** field.

   .. note::
      VLAN names are 'SSLO-INSP-L3-IN' and 'SSLO-INSP-L3-OUT' (but lowercase).

      In the future, the VLAN names will be selectable from a list.

   - Select **ICMP** for the **Device Monitor**.

   .. image:: ./images/service-4.png


#. In the **Inspection Service Endpoints** section (between the **To: VLAN** and **From: VLAN** sections), click the **Start Adding** button.

   .. image:: ./images/service-5.png

   - Enter ``198.19.64.30`` in the **Server Address** field.

   .. image:: ./images/service-6.png


#. Click the **Review & Deploy** button.

#. In the **Deploy Inspection Service** panel, add the BIG-IP Next instance.

   - Click the **Start Adding** button
   - Select the instance named **bigip-next.f5labs.com**.
   - Click on the **+ Add to List** button.

   .. image:: ./images/service-7.png


   - Click the checkbox to the left of the assigned instance and then click the **Validate** button.

     .. image:: ./images/service-8a.png


   - If Validation is successful, click the **Deploy Changes** button to push this inspection service configuration to the BIG-IP Next instance.

     .. image:: ./images/service-8b.png


   - At the **Deploy Inspection Service** prompt, click on the **Deploy Changes** button and wait for the task to complete.


After deployment, the new inspection service will appear in the list.

   .. image:: ./images/service-9.png

