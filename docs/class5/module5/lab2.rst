Defining an Inspection Service
================================================================================


Create an ICAP Inspection Service
--------------------------------------------------------------------------------

Now, you will create an ICAP inspection service.

#. In the **Inspection Services** window, click the **+ Create** button.

#. In the **Create Inspection Service** drawer, select **Generic ICAP** and click the **Start Creating** button.

#. In the subsequent drawer, enter the following:

   - Name: ``my-sslo-icap``
   - Description (optional): ``ICAP service``
   - Request Modification URI Path: ``/avscan``
   - Response Modification URI Path: ``/avscan``

#. Click the **Save & Continue** button.

#. In the **Network** settings, apply the following:

   - VLAN Name: ``sslo-insp-icap``
   - Device Monitor: Select **TCP**
   - Click the **Start Adding** button in the **Endpoints** section
   - Add: ``198.19.97.50``, port ``1344``

#. Click the **Review & Deploy** button.

#. In the **Deploy Inspection Service** drawer, add the BIG-IP Next instance. 

#. Click the checkbox to the left of the assigned instance, then click the **Validate** button.

#. If Validation is Successful, click the **Deploy Changes** button to push this
   inspection service configuration to the BIG-IP Next instance.

