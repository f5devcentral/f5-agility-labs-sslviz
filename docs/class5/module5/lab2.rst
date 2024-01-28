Defining an Inspection Service
================================================================================


Create an ICAP Inspection Service
--------------------------------------------------------------------------------

Now, you will create an ICAP inspection service.

#. In the top left corner of the BIG-IP Central Manager GUI, click on the **Workspace** icon to show the **Workspace Menu**.

#. Click on **Security** to navigate to the Security workspace.

#. In the **SSL Orchestrator** menu, click on **Inspection Services**.

#. Click on **+ Create** to add a new service.

#. In the **Create Inspection Service** panel, select **Generic ICAP** and then click the **Start Creating** button.

   .. image:: ./images/icap-1.png


#. In the **General Properties** section of the **Create Inspection Service: 'Generic ICAP'** panel:

   - Enter ``my-sslo-icap`` in the **Name** field.
   - Enter ``ICAP antivirus scanner`` in the **Description** field (optional).
   - Enter ``/avscan`` in the **Request Modification URI Path** field.
   - Enter ``/avscan`` in the **Response Modification URI Path** field.
   - Click the **Save & Continue** button.

   .. image:: ./images/icap-2.png


#. In the **Network** settings:

   - Enter ``sslo-insp-icap`` in the **VLAN Name** field.
   - Select **TCP** in the **Device Monitor** field.
   - In the **Inspection Service Endpoints** section, click the **Start Adding** button.
   - Enter ``198.19.97.50`` in the **Server Address** field.
   - Enter ``1344`` in the **Port** field.

   .. image:: ./images/icap-3.png

#. Click the **Review & Deploy** button.


#. In the **Deploy Inspection Service** panel, add the BIG-IP Next instance.

   - Click the **Start Adding** button
   - Select the instance named **bigip-next.f5labs.com**.
   - Click on the **+ Add to List** button.



   - Click the checkbox to the left of the assigned instance and then click the **Validate** button.

   - If Validation is successful, click the **Deploy Changes** button to push this inspection service configuration to the BIG-IP Next instance.

     .. image:: ./images/icap-4.png


   - At the **Deploy Inspection Service?** prompt, click on the **Yes, Deploy** button and wait for the task to complete.


After deployment, the new inspection service will appear in the list.

   .. image:: ./images/icap-5.png

